<script>
    let lebronTimeline = [
      { year: "2003", event: "Number 1 overall pick to the Cleveland Cavaliers" },
      { year: "2004", event: "Rookie of the year" },
      { year: "2006", event: "Youngest to ever score 5000 points" },
      { year: "2008", event: "Olympic gold medal" },
      { year: "2009", event: "MVP" },
    ];
  
    let jordanTimeline = [
      { year: "1984", event: "Selected 3rd overall by the Chicago Bulls (College Player of the Year)" },
      { year: "1984", event: "Olympic gold medal" },
      { year: "1985", event: "Rookie of the year" },
      { year: "1985", event: "Shoes in his name (Air Jordans)" },
      { year: "1988", event: "NBA MVP" },
      { year: "1994", event: "Retired from basketball to play baseball" },
      { year: "1996", event: "Space Jam - Hit movie" },
      { year: "2001", event: "Washington Wizards - Tried again but failed" },
      { year: "2009", event: "Hall of Fame" },
    ];
  </script>
  
  <h1 class="body-header">Player Timeline</h1>
  
  <div class="timeline-container">
    <div class="timeline-left">
      <h2>LeBron James</h2>
      <div class="timeline">
        {#each lebronTimeline as item}
          <div class="timeline-item">
            <div class="circle">
              <span class="year">{item.year}</span>
            </div>
            <div class="event-details">
              <span class="event">{item.event}</span>
            </div>
          </div>
        {/each}
      </div>
    </div>
  
    <div class="timeline-right">
      <h2>Michael Jordan</h2>
      <div class="timeline">
        {#each jordanTimeline as item}
          <div class="timeline-item">
            <div class="circle">
              <span class="year">{item.year}</span>
            </div>
            <div class="event-details">
              <span class="event">{item.event}</span>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>
  
  
  
  
  
  <style>
  .body-header {
      text-align: center;
      font-weight: bold; /* Added font-weight: bold */
      font-size: 2.5rem; /* Increased font size */
      margin-bottom: 2rem;
    }
    .timeline-container {
      display: flex;
      justify-content: space-between;
      margin-top: 40px;
    }
  
    .timeline-left h2, .timeline-right h2 {
      text-align: center;
  
      font-size: 2rem; /* Increased font size */
      margin-bottom: 2rem;
    }
    .timeline-item {
      margin-left: 30px; 
      margin-right: 30px;
      display: flex;
      align-items: center;
      margin-bottom: 40px;
    }
  
    .circle {
      width: 60px; 
      height: 60px; 
      background-image: url('https://img2.svgdesigns.com/printart/xlarge/Art_Boutique_Butterfly/PGAB2343.webp');
      background-size: cover;
      border-radius: 50%;
      margin-right: 30px;
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  
    .circle::after {
      content: '';
      position: absolute;
      width: 2px; /* Width of the line */
      height: 100%; /* Height of the line */
      background-color: black; /* Color of the line */
      top: 100%; /* Position below the circle */
      left: 50%; /* Centered horizontally */
      transform: translateX(-50%); /* Centered horizontally */
      z-index: -1; /* Behind the circle */
      
    }
  
    .circle .year {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 14px;
      color: #8B0000 ;
      font-weight: bold;
    }
  
    .event-details {
      display: flex;
      flex-direction: column;
    }
  
    .timeline-item .year {
      font-weight: bold;
      margin-bottom: 5px;
    }
  
    .timeline-item .event {
      margin-bottom: 5px;
    }
  </style>