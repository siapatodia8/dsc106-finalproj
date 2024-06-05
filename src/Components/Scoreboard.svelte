<script>
  import { onMount } from 'svelte';

  let data = [
    { name: "LJ", score: 0 },
    { name: "MJ", score: 0 }
  ];

  let currentTime = "00:00";
  let showScoreboard = false;

  const incrementScore = (index) => {
    data[index].score += 1;
  };

  onMount(() => {
    const mjvsLebronSection = document.getElementById('mjvsLebron');

    const handleScroll = () => {
      if (window.scrollY > mjvsLebronSection.offsetTop) {
        showScoreboard = true;
      } else {
        showScoreboard = false;
      }
    };

    window.addEventListener('scroll', handleScroll);

    return () => {
      window.removeEventListener('scroll', handleScroll);
    };
  });
</script> 

<section id="mjvsLebron">
  test
  
</section>

{#if showScoreboard}
  <div id="scoreboard" class="scoreboard">
    <div class="team">
      <div class="team-name" style="font-size: 48px;">{data[0].name}</div>
      <div class="team-score" style="color: #D22B2B; font-size: 75px;">
        <span class="score-number">{data[0].score}</span>
        <div class="overlay"></div> <!-- Black square with 50% opacity -->
      </div>
      <button on:click={() => incrementScore(0)}>Add 1</button>
    </div>
    <div class="time" style="color: #FFA500; font-size: 68px; border-right: 3px solid white; border-left: 3px solid white; border-bottom: 3px solid white; padding: 20px;">{currentTime.split(':')[0]}<span style="color: white;">:</span>{currentTime.split(':')[1]}</div>
    <div class="overlay2"></div>
    <div class="team">
      <div class="team-name" style="font-size: 48px;">{data[1].name}</div>
      <div class="team-score" style="color: #D22B2B; font-size: 75px;">
        <span class="score-number">{data[1].score}</span>
        <div class="overlay"></div> <!-- Black square with 50% opacity -->
      </div>
      <button on:click={() => incrementScore(1)}>Add 1</button>
    </div>
  </div>
{/if}

<style>
  .scoreboard {
    width: 650px;
    height: 200px;
    text-align: center;
    margin: 0 auto;
    background-color: #0818A8;
    padding: 20px;
    border-radius: 10px;
    position: fixed; 
    top: 0; 
    left: 50%; 
    transform: translateX(-50%); 
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    border: 4px solid #949494;
    z-index: 1000; 
  }

  .team {
    display: flex;
    flex-direction: column;
    width: 150px;
    color: white;
    align-items: center; /* Center align button */
  }

  .team-name {
    font-weight: bold;
    margin-bottom: 10px;
  }

  .team-score {
    font-size: 48px;
    position: relative;
    margin-bottom: 10px; 
  }

  .score-number {
    position: relative; 
  }

  .overlay {
    position: absolute;
    bottom: 5px;
    left: 50%; 
    transform: translateX(-50%); 
    width: 75px; 
    height: 75px; 
    background-color: rgba(0, 0, 0, 0.3); 
    border-radius: 8%; 
  }

  .overlay2 {
    position: absolute;
    top: 18px; 
    left: 50%; 
    transform: translateX(-50%); 
    width: 220px;
    height: 85px; 
    background-color: rgba(0, 0, 0, 0.3); 
    border-radius: 8%; 
  }

  .time {
    font-size: 36px;
    margin-top: -20px;
  }

  button {
    margin-top: 10px; 
    padding: 10px 20px;
    font-size: 16px;
    background-color: #ffa500;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  button:hover {
    background-color: #cc8400;
  }

  #mjvsLebron {
    height: 200px; 
    padding: 20px;
    text-align: center;
  }
</style>

