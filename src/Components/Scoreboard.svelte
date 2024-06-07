<script>
  import { onMount } from 'svelte';
  import * as d3 from 'd3';

  let data = [
    { name: "LJ", score: 0 },
    { name: "MJ", score: 0 }
  ];

  let currentTime = "00:00";

  let quarter = 1;

  function incrementScore(index) {
    data[index].score += 1;
  }

  function decrementScore(index) {
    if (data[index].score > 0) {
      data[index].score -= 1;
    }
  }

  // Define dot positions for LJ and MJ
  const ljDots = [
  // L
  { x: 30, y: 60 },{ x: 30, y: 70 }, { x: 30, y: 80 }, { x: 30, y: 90 }, { x: 30, y: 100 }, { x: 30, y: 110 }, { x: 30, y: 120 }, { x: 30, y: 130 },
  { x: 30, y: 130 }, { x: 40, y: 130 }, { x: 50, y: 130 }, { x: 60, y: 130 },
  // J
  { x: 90, y: 60 }, { x: 100, y: 60 }, { x: 110, y: 60 }, { x: 120, y: 60 }, { x: 130, y: 60 }, { x: 140, y: 60 },
  { x: 115, y: 70 }, { x: 115, y: 80 }, { x: 115, y: 90 }, { x: 115, y: 100 }, { x: 115, y: 110 }, { x: 115, y: 120 }, { x: 115, y: 130 },
  { x: 105, y: 130 }, { x: 95, y: 130 }, { x: 85, y: 130 }, { x: 85, y: 130 }, { x: 85, y: 120 }
];

const mjDots = [
  // M
  { x: 50, y: 130 }, { x: 50, y: 120 }, { x: 50, y: 110 }, { x: 50, y: 100 }, { x: 50, y: 90 }, { x: 50, y: 80 },{ x: 50, y: 70 }, { x: 50, y: 60 },
  { x: 60, y: 65 }, { x: 68, y: 72 }, { x: 76, y: 79}, { x: 86, y: 79}, { x: 94, y: 72},{ x: 102, y: 65},
  { x: 111, y: 60 }, { x: 111, y: 70 }, { x: 111, y: 80 }, { x: 111, y: 90 },{ x: 111, y: 100 }, { x: 111, y: 110 }, { x: 111, y: 120 }, { x: 111, y: 130 },
  // J
  { x: 140, y: 60 }, { x: 150, y: 60 }, { x: 160, y: 60 }, { x: 170, y: 60 }, { x: 180, y: 60 }, { x: 190, y: 60 },
  { x: 165, y: 70 }, { x: 165, y: 80 }, { x: 165, y: 90 }, { x: 165, y: 100 }, { x: 165, y: 110 }, { x: 165, y: 120 }, { x: 165, y: 130 },
  { x: 155, y: 130 }, { x: 145, y: 130 }, { x: 135, y: 130 }, { x: 135, y: 120 }
];


  function drawDots(container, dots) {
    const svg = d3.select(container)
      .attr("width", 200)
      .attr("height", 200);

      svg.selectAll("circle")
      .data(dots)
      .enter()
      .append("circle")
      .attr("cx", d => d.x)
      .attr("cy", d => d.y)
      .attr("r", 3.5) 
      .attr("fill", "white");
  }

  onMount(() => {
    drawDots("#lj-dots", ljDots);
    drawDots("#mj-dots", mjDots);
  });
</script>

<p class="p-left"> Welcome to the ultimate showdown between LeBron James and Michael Jordan! Our interactive scoreboard lets you decide who comes out on top. Add or subtract points for each player as you dive into their stats, achievements, and legendary moments. Every time you see "Who do you think won this round?", cast your vote by adding a point to your favorite. Join the fun and help settle the greatest basketball debate of all time!

</p>

<div id="scoreboard" class="scoreboard">
  <div class="team">
    <svg id="lj-dots" class="dot-matrix"></svg>
    <div class="team-score">
      <span class="score-number dot-matrix">{data[0].score}</span>
      <div class="buttons">
        <button on:click={() => incrementScore(0)}>+</button>
        <button on:click={() => decrementScore(0)}>-</button>
      </div>
    </div>
  </div>

  <div class="center">
    <div class="time dot-matrix">{currentTime.split(':')[0]}<span>:</span>{currentTime.split(':')[1]}</div>
    <div class="quarter">
      <div class="dot-matrix">QTR</div>
      <div class="quarter-number dot-matrix">{quarter}</div>
    </div>
  </div>

  <div class="team">
    <svg id="mj-dots" class="dot-matrix"></svg>
    <div class="team-score">
      <span class="score-number dot-matrix">{data[1].score}</span>
      <div class="buttons">
        <button on:click={() => incrementScore(1)}>+</button>
        <button on:click={() => decrementScore(1)}>-</button>
      </div>
    </div>
  </div>
</div>

<style>
  .scoreboard {
    width: 700px;
    height: 320px;
    margin: 50px auto;
    background-color: black;
    padding: 20px;
    border-radius: 10px;
    position: sticky;
    top: 0;
    z-index: 10;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: 5px solid grey;
    margin-top: 90px;
  }

  .team {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 200px;
    color: white;
  }

  .team-score {
    font-size: 80px;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 40px;
  }

  .score-number {
    margin-bottom: 25px;
    border: 2px solid white;
    padding-left: 10px;
    padding-right: 10px;
    border-radius: 10px;
  }

  .buttons {
    display: flex;
    gap: 5px;
    margin-top: -20px;
  }

  .time {
    font-size: 58px;
    color: red;
    margin-bottom: 20px;
    border: 2px solid white;
    padding: 10px;
    border-radius: 10px;
  }

  .quarter {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .quarter-number {
    font-size: 48px;
    margin-bottom: 10px;
  }

  button {
    font-size: 24px;
    padding: 5px 10px;
    cursor: pointer;
    background-color: black;
    border: none;
    border-radius: 5px;
    color: white;
  }

  button:hover {
    background-color: #ddd;
  }

  p {
  text-align: center; 
  max-width: 700px; 
  margin: 0 auto; 
  margin-top: 90px;
}

/* .p-left {
  text-align: left;
} */

</style>
