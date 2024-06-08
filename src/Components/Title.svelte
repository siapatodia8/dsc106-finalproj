<section id="intro" class="centered-section">
  <div class="basketball-container">
    <svg id="basketball" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 800"> 
      <circle cx="400" cy="400" r="375" fill="orange" stroke="black" stroke-width="4"/> 
    </svg>
    <!-- Larger basket -->
    <svg id="basket" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 800"> <!-- Adjusted viewBox size -->
      <rect x="50" y="450" width="750" height="40" fill="brown"/> <!-- Adjusted dimensions -->
      <line x1="50" y1="450" x2="1200" y2="450" stroke="black" stroke-width="12"/> <!-- Adjusted dimensions -->
    </svg>
  </div>
  <h1 id="intro-hed">Who's The NBA G.O.A.T. ?</h1>
  <br><br>
  <h3 id="intro__date">
    <a  target="_blank"><b>Jovanna Fernando, Lewis Weng, Sia Patodia </b></a> <br>May, 2024
  </h3>
</section>

<p class="p-left" >
  <br><br><br>
  When discussing basketball’s greatest of all times, 2 names are often brought up:
  Michael Jordan and LeBron James. Before James, Jordan was the undisputed best basketball
  player to grace the court. In Jordan’s 13 years of playing basketball, he has made 6 finals
  and won all 6 of them, with both of them being a 3-peat. Not only did he win 6 out of 6 finals,
  he was also named the Finals MVP in all of them and won multiple MVPs during this time. 

  <br><br>In both of their careers, it is undeniable that both players were key towards their teams’ success and that those teams
  wouldn’t have won those titles without them. In our website, we will compare the in-game statistics between these 2 GOAT
  candidates to weigh their contributions to their team.
  <br><br><br>
</p>

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
    height: 100px; /* Adjusted height */
    margin-bottom: 20px;
  }

  .basketball-container #basketball {
    position: absolute;
    left: 25px;
    width: 50px;
    height: 80px;
    animation: drop 0.8s ease-in-out infinite;
    animation-play-state: paused;
}

  #basket {
    position: absolute;
    bottom: -10;
    left: 0;
    width: 100px;
    height: 100px;
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
      top: 60px;
    }
    100% {
      top: 60px;
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
    const basketball = document.getElementById('basketball');
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


