<section id="intro" class="centered-section">
  <div class="basketball-container">
    <svg id="basketball" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 50 50">
      <circle cx="25" cy="25" r="20" fill="orange" stroke="black" stroke-width="2"/>
    </svg>
    <svg id="basket" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100">
      <rect x="20" y="80" width="60" height="10" fill="brown"/>
      <line x1="20" y1="80" x2="80" y2="80" stroke="black" stroke-width="2"/>
    </svg>
  </div>
  <h1 id="intro-hed">Who's The NBA G.O.A.T. ?</h1>
  <br><br>
  <h3 id="intro__date">
    <a  target="_blank"><b>Jovanna Fernando, Lewis Weng, Sia Patodia </b></a> <br>May, 2024
  </h3>
</section>

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
    width: 100px;
    height: 100px;
    margin-bottom: 20px;
  }

  #basketball {
    position: absolute;
    top: -20px;
    left: 25px;
    width: 50px;
    height: 50px;
    animation: drop 1s ease-in-out infinite;
    animation-play-state: paused;
  }

  #basket {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100px;
    height: 100px;
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

