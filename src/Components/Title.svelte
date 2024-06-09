<section id="intro" class="centered-section">
  <div class="basketball-container">
    <!-- New basketball SVG -->
    <svg id="ball" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 50 50" class="noSelect">
      <defs>
        <clipPath id="clip-path">
          <circle cx="25" cy="25" r="24"/>
        </clipPath>
      </defs>
      <title>Basketball</title>
      <circle cx="25" cy="25" r="24" fill="#ee6730"/>
      <g class="ballPath" stroke="black" stroke-width="0.8" fill="none">
        <path class="ballStripe" d="M6,10a22,22,0,0,1,8-1.8c4-.2,7.8,1,11.2,2.1s4.4,1.5,7.6,1.7,3.8-.2,4.8-.7a6,6,0,0,0,2.3-2.7"/>
        <path class="ballStripe" d="M26.4,3c2.4,2,7.8,7.3,9.1,15.5C37,31,26.8,41,25.6,42.5"/>
        <path class="ballStripe" d="M4,26.5a60,60,0,0,1,22-8,60,60,0,0,1,20.6,.5"/>
        <path class="ballStripe" d="M8,37.3a28.5,28.5,0,0,0,6-2.4c7.8-4.1,8.5-9.2,16.8-13,3.5-1.6,5.6-1.7,6.8-1.5,4.6.4,7,3.6,7.3,4.1,2.7,3.9.6,7.8.3,8.4"/>
      </g>
    </svg>           
    
    
    <!-- New basket SVG -->
    <svg id="basket" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 120 90" preserveAspectRatio="xMidYMin">
      <g id="net">
        <line x1="33" y1="76" x2="74.1" y2="117.1" stroke="#888" stroke-width="0.5"/>
        <line x1="87" y1="76" x2="45.6" y2="117.4" stroke="#888" stroke-width="0.5"/>
        <line x1="78.3" y1="73.8" x2="43.2" y2="109" stroke="#888" stroke-width="0.5"/>
        <line x1="68.1" y1="73.8" x2="41.9" y2="100" stroke="#888" stroke-width="0.5"/>
        <line x1="58.2" y1="73.8" x2="39.5" y2="92.5" stroke="#888" stroke-width="0.5"/>
        <line x1="47.4" y1="73.8" x2="36.5" y2="84.7" stroke="#888" stroke-width="0.5"/>
        <line x1="40.7" y1="73.5" x2="76.3" y2="109.1" stroke="#888" stroke-width="0.5"/>
        <line x1="51.6" y1="73.8" x2="77.7" y2="99.9" stroke="#888" stroke-width="0.5"/>
        <line x1="61.9" y1="73.8" x2="80.4" y2="92.3" stroke="#888" stroke-width="0.5"/>
        <line x1="72.2" y1="73.8" x2="82.7" y2="84.3" stroke="#888" stroke-width="0.5"/>
        <line x1="39.5" y1="92.5" x2="64.1" y2="117.2" stroke="#888" stroke-width="0.5"/>
        <line x1="42.7" y1="106.3" x2="54.5" y2="118.1" stroke="#888" stroke-width="0.5"/>
        <line x1="80.4" y1="92.3" x2="54.5" y2="118.1" stroke="#888" stroke-width="0.5"/>
        <line x1="77.3" y1="105.8" x2="65.7" y2="117.4" stroke="#888" stroke-width="0.5"/>
    </g>       
      <rect id="ring" x="28" y="70" width="64" height="6" rx="3" fill="#A52A2A" stroke="black" stroke-width="0.5"/>
    </svg>
  </div>
  
  <h1 id="intro-hed">Who's The NBA G.O.A.T. ?</h1>
  <br><br>
  <h3 id="intro__date">
    <a target="_blank"><b>Jovanna Fernando, Lewis Weng, Sia Patodia </b></a> <br>May, 2024
  </h3>
</section>

<p class="p-left">
  <br><br><br>
  When discussing basketball’s greatest of all times, 2 names are often brought up:
  Michael Jordan and LeBron James. Before James, Jordan was the undisputed best basketball
  player to grace the court. In Jordan’s 13 years of playing basketball, he has made 6 finals
  and won all 6 of them, with both of them being a 3-peat. Not only did he win 6 out of 6 finals,
  he was also named the Finals MVP in all of them and won multiple MVPs during this time. 

  <br><br>In both of their careers, it is undeniable that both players were key towards their teams’ success and that those teams
  wouldn’t have won those titles without them. In our website, we will compare the in-game statistics between these 2 GOAT
  candidates to weigh their contributions to their team. For more info check out our 
  <a href="https://www.youtube.com/watch?v=Zas3KIQQ1gc">video</a>.
</p>
<br><br><br><br>

<style>
  #intro {
    max-width: 800px;
    min-height: 300px;
    margin: auto;
    text-align: center;
    padding-top: 1rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  #intro-hed {
    font-size: 4rem;
    margin-top: 5px;
    margin-bottom: 0;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    max-width: 100%;
    color: var(--squid-ink);
  }

  #intro__date {
    font-size: 1.1rem;
    color: var(--squid-ink);
    margin: 0px;
    margin-top: 15px;
    padding-bottom: 0px;
    margin-bottom: 0px;
    color: black;
    padding-bottom: 1rem;
    font-family: var(--font-main);
  }

  .basketball-container {
    position: relative;
    width: 200px; /* Adjusted width */
    height: 200px; /* Adjusted height */
    margin-bottom: 20px;
  }

  .basketball-container #ball {
    position: absolute;
    left: 50px;
    top: 0;
    width: 100px;
    height: 100px;
    animation: drop 0.8s ease-in-out infinite;
    animation-play-state: paused;
  }

  .basketball-container #basket {
    position: absolute;
    bottom: 0;
    left: -25px;
    width: 250px;
    height: 250px;
  }

  p {
    text-align: center; 
    max-width: 700px; 
    margin: 0 auto; 
  }

  @keyframes drop {
    0% {
      top: -20px;
    }
    70% {
      top: 100px;
    }
    100% {
      top: 100px;
    }
  }

  /* mobile */
  @media screen and (max-width: 950px) {
    #intro-hed {
      font-size: 3.5rem;
    }

    .intro-sub {
      font-size: 1.5rem;
    }
  }
</style>

<script>
  import { onMount } from 'svelte';

  onMount(() => {
    const basketball = document.getElementById('ball');
    function startAnimation() {
      basketball.style.animationPlayState = 'running';
      setTimeout(() => {
        basketball.style.animationPlayState = 'paused';
      }, 1000);
    }
    startAnimation();
    setInterval(startAnimation, 3000);
  });
</script>