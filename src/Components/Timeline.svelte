<script>
  let lebronTimeline = [
    { year: "1984", event: "" },
    { year: "1984", event: "" },
    { year: "1985", event: "" },
    { year: "1985", event: "" },
    { year: "1988", event: "" },
    { year: "1994", event: "" },
    { year: "1996", event: "" },
    { year: "2001", event: "" },
    { year: "2003", event: "Number 1 overall pick to the Cleveland Cavaliers" },
    { year: "2004", event: "Rookie of the year"},
    { year: "2006", event: "Youngest to ever score 5000 points" },
    { year: "2008", event: "Olympic gold medal" },
    { year: "2009", event: "MVP" }
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
    { year: "2003", event: "" },
    { year: "2004", event: "" },
    { year: "2006", event: "" },
    { year: "2008", event: "" },
    { year: "2009", event: "Hall of Fame" }
  ];
</script>



<div class="timeline-container">
  <div class="timeline-center">
    <div class="timeline">
      {#each lebronTimeline as item}
        <div class="timeline-item">
          <div class="circle1 {item.event === '' ? 'empty' : ''}">
            <span class="year">{item.year}</span>
          </div>
          <div class="event-details">
            <span class="event">{item.event}</span>
          </div>
        </div>
      {/each}
    </div>
  </div>

  <div class="timeline-center">
    <div class="timeline">
      {#each jordanTimeline as item}
        <div class="timeline-item">
          <div class="circle2 {item.event === '' ? 'empty' : ''}">
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
    font-weight: bold;
    font-size: 2.5rem;
    margin-bottom: 2rem;
  }

  .timeline-container {
    display: flex;
    justify-content: center;
    margin-top: 40px;
    min-height: 100vh; /* Ensure the container takes at least the full viewport height */
  }

  .timeline-center {
    width: 50%;
  }

  .timeline-item {
    margin-left: 30px;
    margin-right: 30px;
    display: flex;
    align-items: center;
    margin-bottom: 40px;
    position: relative;
  }

  .circle1,
  .circle2 {
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
    opacity: 1;
  }

  .circle1::after,
  .circle2::after {
    content: '';
    position: absolute;
    width: 2px;
    height: 50vh; /* Stretch the line to cover the entire viewport height */
    background-color: black;
    top: 0vh; /* Position the line so it extends above and below the circles */
    left: 50%;
    transform: translateX(-50%);
    z-index: -1;
  }

  

  .circle1.empty,
  .circle2.empty {
    opacity: 0;
  }

  .circle1 .year,
  .circle2 .year {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 14px;
    font-weight: bold;
    color: black; /* Default color */
  }

  .event-details {
    display: flex;
    flex-direction: column;
    z-index: 1;
  }

  .timeline-item .year {
    font-weight: bold;
    margin-bottom: 5px;
  }

  .timeline-item .event {
    margin-bottom: 5px;
  }
</style>
