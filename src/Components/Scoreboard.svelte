<script>
  import { onMount } from 'svelte';
  import * as d3 from 'd3';

  let data = [
    { name: "LJ", score: 0 },
    { name: "MJ", score: 0 }
  ];

  let currentTime = "12:07";
  let quarter = 3;

  function incrementScore(index) {
    data[index].score += 1;
  }

  function decrementScore(index) {
    if (data[index].score > 0) {
      data[index].score -= 1;
    }
  }

  const ljDots = [
  { x: 80, y: 20 }, { x: 80, y: 25 }, { x: 80, y: 30 }, { x: 80, y: 35 }, { x: 80, y: 40 }, { x: 80, y: 45 }, { x: 80, y: 50 }, { x: 80, y: 55 },
  { x: 80, y: 55 }, { x: 85, y: 55 }, { x: 90, y: 55 }, { x: 95, y: 55 },
  { x: 110, y: 20 }, { x: 115, y: 20 }, { x: 120, y: 20 }, { x: 125, y: 20 }, { x: 130, y: 20 }, { x: 135, y: 20 },
  { x: 122.5, y: 25 }, { x: 122.5, y: 30 }, { x: 122.5, y: 35 }, { x: 122.5, y: 40 }, { x: 122.5, y: 45 }, { x: 122.5, y: 50 }, { x: 122.5, y: 55 },
  { x: 117.5, y: 55 }, { x: 112.5, y: 55 }, { x: 107.5, y: 55 }, { x: 107.5, y: 50 }
];

const mjDots = [
  { x: 65, y: 55 }, { x: 65, y: 50 }, { x: 65, y: 45 }, { x: 65, y: 40 }, { x: 65, y: 35 }, { x: 65, y: 30 }, { x: 65, y: 25 }, { x: 65, y: 20 },
  { x: 70, y: 22 }, { x: 73, y: 27 }, { x: 76, y: 32 }, { x: 81, y: 32 }, { x: 84, y: 27 }, { x: 87, y: 22 },
  { x: 90, y: 20 }, { x: 90, y: 25 }, { x: 90, y: 30 }, { x: 90, y: 35 }, { x: 90, y: 40 }, { x: 90, y: 45 }, { x: 90, y: 50 }, { x: 90, y: 55 },
  { x: 105, y: 20 }, { x: 110, y: 20 }, { x: 115, y: 20 }, { x: 120, y: 20 }, { x: 125, y: 20 }, { x: 130, y: 20 },
  { x: 117.5, y: 25 }, { x: 117.5, y: 30 }, { x: 117.5, y: 35 }, { x: 117.5, y: 40 }, { x: 117.5, y: 45 }, { x: 117.5, y: 50 }, { x: 117.5, y: 55 },
  { x: 112.5, y: 55 }, { x: 107.5, y: 55 }, { x: 102.5, y: 55 }, { x: 102.5, y: 50 }
];


const qtrDots = [
  // Q
  { x: 60, y: 170 }, { x: 65, y: 170 }, { x: 70, y: 170 }, { x: 75, y: 170 }, { x: 75, y: 175 }, { x: 75, y: 180 }, { x: 75, y: 185 },
  { x: 70, y: 190 }, { x: 65, y: 190 }, { x: 60, y: 190 }, { x: 60, y: 185 }, { x: 60, y: 180 },  { x: 60, y: 175 },
  { x: 70, y: 185 }, { x: 75, y: 190 }, { x: 79, y: 193 },
  // T
  { x: 90, y: 170 }, { x: 95, y: 170 }, { x: 100, y: 170 }, { x: 105, y: 170 }, { x: 110, y: 170 },
  { x: 100, y: 175 }, { x: 100, y: 180 }, { x: 100, y: 185 }, { x: 100, y: 190 },
  // R
  { x: 120, y: 170 }, { x: 125, y: 170 }, { x: 130, y: 170 }, { x: 135, y: 175 }, { x: 135, y: 180 }, { x: 130, y: 180 }, { x: 134, y: 171 },
  { x: 125, y: 180 }, { x: 120, y: 180 }, { x: 120, y: 185 }, { x: 125, y: 185 }, { x: 130, y: 185 }, { x: 135, y: 192 }, { x: 133.5, y: 188 },
  { x: 120, y: 190 }, { x: 120, y: 175 }
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
      .attr("r", 2.4) 
      .attr("fill", "white");
  }

  onMount(() => {
    drawDots("#lj-dots", ljDots);
    drawDots("#mj-dots", mjDots);
    drawDots("#qtr-dots", qtrDots);
  });
</script>

<!-- <h3> Welcome to the ultimate showdown between LeBron James and Michael Jordan!</h3> -->

<div class="marquee-container">
  <h3 class="marquee">Welcome to the ultimate showdown between LeBron James and Michael Jordan! Welcome to the ultimate showdown between LeBron James and Michael Jordan! Welcome to the ultimate showdown between LeBron James and Michael Jordan! Welcome to the ultimate showdown between LeBron James and Michael Jordan! Welcome to the ultimate showdown between LeBron James and Michael Jordan! Welcome to the ultimate showdown between LeBron James and Michael Jordan! Welcome to the ultimate showdown between LeBron James and Michael Jordan! </h3>
</div>

<p class="p-left"> Our interactive scoreboard lets you decide who comes out on top. Add or subtract points for each player as you dive into their stats, achievements, and legendary moments. Every time you see "<strong>Who won this quarter?</strong>", cast your vote by adding a point to your favorite. Join the fun and help settle the greatest basketball debate of all time!</p>


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
      <svg id="qtr-dots" class="dot-matrix" width="200" height="100"></svg>
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
    width: 400px;
    height: 180px;
    margin: 50px auto;
    background-color: black;
    border-radius: 10px;
    position: sticky;
    top: 0;
    z-index: 20;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: 5px solid grey;
    opacity: 0.82;
  }

  .team {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 80px;
    color: white;
  }

  .team-score {
    font-size: 50px;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: -130px;
  }

  .score-number {
    margin-bottom: 25px;
    border: 2px solid white;
    padding-left: 5px;
    padding-right: 5px;
    border-radius: 10px;
  }

  .buttons {
    display: flex;
    gap: 5px;
    margin-top: -20px;
  }

  button {
    font-size: 14px;
    padding: 5px 10px;
    cursor: pointer;
    background-color: black;
    border: none;
    border-radius: 5px;
    color: white;
  }

  .time {
      display: inline-block;
      font-size: 40px;
      color: red;
      border: 2px solid white;
      border-radius: 10px;
      text-align: center;
      padding: 2px 10px; /* Adjust padding to reduce space */
      margin: 0;
      line-height: 1.2; /* Adjust line-height to control vertical spacing */
      box-sizing: border-box;
      margin-left: 35px; 
    }

  .quarter {
    display: flex;
    flex-direction: column;
    align-items: center;
    color: white;
    margin-top: -150px; 
    font-size: 40px;
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

  /* h3 {
    text-align: center;
    max-width: 90%;
    margin: 0 auto;
    margin-top: 90px;
    font-size: 60px;
    color: #D57428; text-shadow: 0 0 3px #FFCC00;
  } */

  .marquee-container {
            width: 100%;
            overflow: hidden;
            white-space: nowrap;
            box-sizing: border-box;
        }
        .marquee {
            display: inline-block;
            padding-left: 10%;
            animation: marquee 55s linear infinite;
            color: #D57428; 
            text-shadow: 0 0 18px #FFCC00;
            font-size: 60px;
        }
        @keyframes marquee {
            0% {
                transform: translateX(0%);
            }
            100% {
                transform: translateX(-100%);
            }
        }
</style>
