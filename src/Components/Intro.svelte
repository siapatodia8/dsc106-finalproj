<script>
  import { onMount } from 'svelte';

  let data = [
    { name: "LJ", score: 0 },
    { name: "MJ", score: 0 }
  ];

  let currentTime = "00:00";

  // onMount(() => {
  //   // Example: Update scores after 2 seconds
  //   setTimeout(() => {
  //     data[0].score = 10;
  //     data[1].score = 5;
  //   }, 2000);
  // });
</script>

<section>

  <div id="scoreboard" class="scoreboard">
    <div class="team">
      <div class="team-name" style="font-size: 48px;">{data[0].name}</div>
      <div class="team-score" style="color: #D22B2B; font-size: 75px;">
        <span class="score-number">{data[0].score}</span>
        <div class="overlay"></div> <!-- Black square with 50% opacity -->
      </div>
    </div>
    <div class="time" style="color: #FFA500; font-size: 68px; border-right: 3px solid white; border-left: 3px solid white; border-bottom: 3px solid white; padding: 20px;">{currentTime.split(':')[0]}<span style="color: white;">:</span>{currentTime.split(':')[1]}</div>
    <div class="overlay2"></div>
    <div class="team">
      <div class="team-name" style="font-size: 48px;">{data[1].name}</div>
      <div class="team-score" style="color: #D22B2B; font-size: 75px;">
        <span class="score-number">{data[1].score}</span>
        <div class="overlay"></div> <!-- Black square with 50% opacity -->
      </div>
    </div>
  </div>

  <style>
    .scoreboard {
      width: 650px;
      height: 200px;
      text-align: center;
      margin: 50px auto 0;
      background-color: #0818A8;
      padding: 20px;
      border-radius: 10px;
      position: relative;
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      border: 4px solid #949494;
    }

    .team {
      display: flex;
      flex-direction: column;
      width: 150px;
      color: white;
    }

    .team-name {
      font-weight: bold;
      margin-bottom: 10px;
    }

    .team-score {
      font-size: 48px;
      position: relative; /* Necessary for overlay */
    }

    .score-number {
      position: relative; /* Necessary for overlay */
    }

    .overlay {
      position: absolute;
      bottom: 5px; /* Adjust as needed */
      left: 50%; /* Center the overlay */
      transform: translateX(-50%); /* Center the overlay */
      width: 75px; /* Adjust width as needed */
      height: 75px; /* Adjust height as needed */
      background-color: rgba(0, 0, 0, 0.3); /* Black with 50% opacity */
      border-radius: 8%; /* Round the edges */
    }

    .overlay2 {
      position: absolute;
      top: 18px; /* Adjust as needed */
      left: 50%; /* Center the overlay */
      transform: translateX(-50%); /* Center the overlay */
      width: 220px; /* Adjust width as needed */
      height: 85px; /* Adjust height as needed */
      background-color: rgba(0, 0, 0, 0.3); /* Black with 50% opacity */
      border-radius: 8%; /* Round the edges */
    }

    .time {
      font-size: 36px;
      margin-top: -20px;
    }
  </style>
</section>
