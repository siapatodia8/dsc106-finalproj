<script>
  let Timeline = [
    { year: "1983", lebron: "", jordan: "College basketball national player of the year", funfact: "testing 123" },
    { year: "1984", lebron: "", jordan: "3rd overall pick to the Chicago Bulls + Olympic gold medal", funfact: "" },
    { year: "1985", lebron: "", jordan: "Rookie of the year + Air Jordans released", funfact: "" },
    { year: "1988", lebron: "", jordan: "NBA MVP and Defensive Player of the Year", funfact: "" },
    { year: "1992", lebron: "", jordan: "Dream Team Gold Medal", funfact: "" },
    { year: "1993", lebron: "", jordan: "Retired to pursue Baseball", funfact: "" },
    { year: "1995", lebron: "", jordan: "Returned to the NBA", funfact: "'I’m back'" },
    { year: "1996", lebron: "", jordan: "Featured in Space Jam", funfact: "" },
    { year: "2003", lebron: "1st overall pick to the Cleveland Cavaliers", jordan: "Officially retired", funfact: "" },
    { year: "2004", lebron: "Rookie of the year", jordan: "", funfact: "" },
    { year: "2006", lebron: "Youngest to ever score 5000 points", jordan: "", funfact: "" },
    { year: "2008", lebron: "Olympic gold medal and Becomes Cavs’ all-time leading scorer", jordan: "", funfact: "" },
    { year: "2009", lebron: "First out of four NBA Most Valuable Player", jordan: "Induction into the basketball Hall of Fame", funfact: "" },
    { year: "2012", lebron: "Sports Illustrated Sportsperson of the Year", jordan: "", funfact: "testing 124" },
    { year: "2016", lebron: "", jordan: "Presidential Medal of Freedom", funfact: "" },
    { year: "2018", lebron: "LeBron’s double-digit scoring record", jordan: "", funfact: "" },
    { year: "2021", lebron: "Featured in Space Jam 2", jordan: "", funfact: "" },
    { year: "2023", lebron: "LeBron becomes NBA’s all-time leading scorer", jordan: "", funfact: "" }
  ];

  let tooltipText = "";
  let hoveredIndex = -1;
  let tooltipHeading = "";

  function showTooltip(index, item) {
    if (item.funfact !== "") {
      tooltipText = item.funfact;
      hoveredIndex = index;
      tooltipHeading = item.lebron ? item.lebron : item.jordan;
    }
  }

  function hideTooltip() {
    tooltipText = "";
    hoveredIndex = -1;
    tooltipHeading = "";
  }
</script>



<div class="timeline-container">
  <div class="timeline">
    {#each Timeline as item, index}
      <div class="timeline-item">
        <div class="event-details left">
          <span class="event">{item.lebron}</span>
        </div>
        <div 
          class="circle {item.funfact ? 'has-funfact' : ''}" 
          style="background-image: url('https://st2.depositphotos.com/2485347/5763/v/450/depositphotos_57633389-stock-illustration-basketball-ball.jpg')"
          on:mouseover={() => showTooltip(index, item)}
          on:mouseout={() => hideTooltip()}
        >
          <span class="year">{item.year}</span>
          {#if hoveredIndex === index && item.funfact}
            <div class="tooltip">
              <h3>{tooltipHeading}</h3>
              <p><br><br><br>{tooltipText}</p>
            </div>
          {/if}
        </div>
        <div class="event-details right">
          <span class="event">{item.jordan}</span>
        </div>
      </div>
    {/each}
  </div>
</div>
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

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
  }

  .timeline {
    display: flex;
    flex-direction: column;
    position: relative; 
  }

  .tooltip {
    position: absolute;
    background-color: rgba(255, 253, 253, 1); 
    color: black;
    padding: 15px 20px;
    border-radius: 5px;
    border: 1px solid black;
    pointer-events: none;
    z-index: 9999;
    width: 900px; /* Increased width for a larger tooltip box */
    height: 500PX;
    top: 70px; /* Position the tooltip below the circle */
    left: 50%;
    transform: translateX(-50%);
  }

  .tooltip h3 {
    font-size: 1rem;
    font-weight: bold;
    margin: 0 0 10px 0;
    text-decoration: underline;
    text-align: center;
  
  }

  .tooltip p {
    margin: 0;
    text-align: center;
  }

  .timeline-item {
    display: flex;
    align-items: center;
    margin-bottom: 40px;
  }

  .event-details {
    flex: 1;
  }

  .circle {
    position: relative;
    width: 60px;
    height: 60px;
    border-radius: 60%;
    background-size: cover;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }

  .circle.has-funfact {
    border: 3px solid rgb(239, 239, 63); 
  }

  .circle .year {
    position: absolute;
    font-size: 14px;
    font-weight: bold;
    color: white;
  }

  .event-details {
    flex: 1;
    text-align: center; 
    padding: 0 30px;
  }

  @media (max-width: 768px) {
    .timeline-item {
      flex-direction: column;
      align-items: center;
    }

    .event-details {
      text-align: center;
      margin-bottom: 10px;
    }
  }
</style>

