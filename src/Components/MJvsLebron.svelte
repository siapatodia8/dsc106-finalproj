<script>
    import Scrolly from "./Scrolly.svelte";
    import katexify from "../katexify";
    import { select, selectAll } from "d3-selection";
  
    let value;
  
    $: steps = [
      `<h1 class='step-title'>stat 1</h1>
       <br><br>
       <p>will contain important information about LeBron James and Michael Jordan.<br><br>
       Example: all-time stats, all-star games, MVPs, impact on sales</p>`,
      `<h1 class='step-title'>stat 2</h1>
       <p>Content for stat 2.</p>
       <br><br>`,
      `<h1 class='step-title'>stat 3</h1>
       <p>Content for stat 3.</p>
       <br><br>`,
      `<h1 class='step-title'>stat 4</h1>
       <p>Content for stat 4.</p>
       <br><br>`,
    ];
  
    $: if (typeof value !== "undefined") target2event[value]();
  
    // Assuming target2event is defined somewhere, otherwise define it like this:
    const target2event = {
      0: () => console.log("Stat 1 action"),
      1: () => console.log("Stat 2 action"),
      2: () => console.log("Stat 3 action"),
      3: () => console.log("Stat 4 action"),
    };
  </script>
  
  <section class="header-section">
    <div class="name-container">
      <span class="player-name">LeBron</span>
      <span class="vs">vs</span>
      <span class="player-name">Jordan</span>
    </div>
  </section>
  
  <section>
    <div class="section-container">
      <div class="image-container">
        <img id="chart2" src="https://www.freeiconspng.com/thumbs/lebron-james-png/lebron-james-png-8.png" alt="LeBron James image">
      </div>
      <div class="steps-container">
        <Scrolly bind:value>
          {#each steps as text, i}
            <div class="step" class:active={value === i}>
              <div class="step-content">{@html text}</div>
            </div>
          {/each}
          <div class="spacer"></div>
        </Scrolly>
      </div>
      <div class="image-container">
        <img id="chart3" src="https://www.pngall.com/wp-content/uploads/5/Michael-Jordan-Basketball-Player-Transparent.png" alt="Michael Jordan image">
      </div>
    </div>
    <br /><br />
    <p class="body-text"></p>
  </section>
  
  <style>
  .header-section {
      text-align: center;
      margin-bottom: 1rem;
    }
  
    .name-container {
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 2rem;
    }
  
    .player-name {
      font-size: 2.5rem;
      font-weight: bold;
      margin: 0 14rem;
    }
  
    .vs {
      font-size: 2rem;
      margin: 0 14rem;
    }
  
    .image-container img {
      width: 100%;
      max-width: 1000px;
      display: block;
      margin: 1rem 0;
      opacity: 0.8;
    }
  
    .spacer {
      height: 0vh;
    }
  
    .section-container {
      margin-top: 0em;
      text-align: center;
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
    }
  
    .step {
      height: 40vh; /* CHANGES SPACING BETWEEN THE STATS!! */
      display: flex;
      align-items: center;
      justify-content: center;
    }
  
    
  
    .step-content {
      font-size: 18px;
      background: var(--bg);
      color: #ccc;
      border-radius: 1px;
      padding: 0.5rem 1rem;
      display: flex;
      flex-direction: column;
      justify-content: center;
      transition: background 500ms ease;
      text-align: left;
      width: 75%;
      margin: auto;
      max-width: 700px;
      font-family: var(--font-main);
      line-height: 1.3;
      border: 1px solid var(--default);
      margin-bottom: 1rem;
      min-height: 100px;
    }
  
    .step.active .step-content {
      background: #f1f3f3ee;
      color: var(--squid-ink);
    }
  
    .steps-container {
      height: 100%;
      flex: 1 1 40%;
      z-index: 10;
    }
  
    .image-container {
      flex: 1 1 20%;
      position: sticky;
      top: 10%;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
  
    @media screen and (max-width: 950px) {
      .section-container {
        flex-direction: column;
      }
  
      .steps-container {
        pointer-events: none;
      }
  
      .image-container {
        width: 100%;
        margin: none;
        position: static;
      }
  
      .step {
        height: 130vh;
      }
  
      .step-content {
        width: 95%;
        max-width: 768px;
        font-size: 17px;
        line-height: 1.6;
      }
  
      .spacer {
        height: 100vh;
      }
  
      .image-container img {
        max-width: 150px; 
      }
    }
  </style>