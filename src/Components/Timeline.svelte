<script>
  let Timeline = [
    { year: "1983", lebron: "", jordan: "College basketball national player of the year", funfact: "" },
    { year: "1984", lebron: "", jordan: "3rd overall pick to the Chicago Bulls + Olympic gold medal", funfact: "" },
    { year: "1985", lebron: "", jordan: "Rookie of the year + Air Jordans released", funfact: "" },
    { year: "1988", lebron: "", jordan: "NBA MVP and Defensive Player of the Year", funfact: "" },
    { year: "1992", lebron: "", jordan: "Dream Team Gold Medal", funfact: "As a member of the 'Dream Team,' Michael Jordan won a gold medal at the 1992 Barcelona Olympics. This team, which included legends like Magic Johnson, Larry Bird, and Charles Barkley, is widely regarded as the best basketball team ever assembled. Jordan's leadership and stellar play were instrumental in the team's dominant performance, winning every game by a significant margin. The Dream Team not only captured the gold medal but also played a crucial role in popularizing basketball worldwide, inspiring a new generation of players and fans globally. This achievement was a highlight of Jordan’s career and underscored his global impact on the sport." },
    { year: "1993", lebron: "", jordan: "Retired to pursue Baseball", funfact: "" },
    { year: "1995", lebron: "", jordan: "Returned to the NBA", funfact: "After a brief retirement and an attempt at a baseball career, Michael Jordan's return to the NBA in 1995 was one of the most highly anticipated comebacks in sports history. His two-word press release, 'I'm back,' sent shockwaves through the sports world, reigniting excitement among fans and media alike. Jordan’s return revitalized the Chicago Bulls, leading them to three more consecutive NBA championships and solidifying his legacy as the greatest basketball player of all time. This comeback not only demonstrated his unparalleled competitive spirit but also his ability to perform at the highest level after a significant hiatus, further enhancing his legendary status." },
    { year: "1996", lebron: "", jordan: "Featured in Space Jam", funfact: "In 1996, Michael Jordan starred in the live-action/animated film 'Space Jam.' The movie became a cultural phenomenon, blending basketball with popular culture and featuring Jordan alongside beloved Looney Tunes characters. 'Space Jam' was more than just a box office success; it was a significant part of Jordan’s legacy, showcasing his crossover appeal and influence beyond the basketball court. The film's success highlighted Jordan’s marketability and the fusion of sports and entertainment, further cementing his status as a global icon. 'Space Jam' remains a beloved classic, symbolizing Jordan’s broad impact on popular culture." },
    { year: "2003", lebron: "1st overall pick to the Cleveland Cavaliers", jordan: "Officially retired", funfact: "" },
    { year: "2004", lebron: "Rookie of the year", jordan: "", funfact: "" },
    { year: "2006", lebron: "Youngest to ever score 5000 points", jordan: "", funfact: "" },
    { year: "2008", lebron: "Olympic gold medal and Becomes Cavs’ all-time leading scorer", jordan: "", funfact: "In 2008, LeBron James had a monumental year. He won an Olympic gold medal with Team USA at the Beijing Olympics, reinforcing his status as one of the top players in the world. That same year, he became the all-time leading scorer for the Cleveland Cavaliers, surpassing Brad Daugherty’s record. These achievements underscored his leadership qualities and his ability to perform on both national and international stages." },
    { year: "2009", lebron: "First out of four NBA Most Valuable Player", jordan: "Induction into the basketball Hall of Fame", funfact: "" },
    { year: "2012", lebron: "Sports Illustrated Sportsperson of the Year", jordan: "", funfact: "" },
    { year: "2016", lebron: "", jordan: "Presidential Medal of Freedom", funfact: "" },
    { year: "2018", lebron: "LeBron’s double-digit scoring record", jordan: "", funfact: "In 2018, LeBron James set the record for the most consecutive games with at least 10 points, surpassing Michael Jordan's previous record. This achievement was a testament to LeBron's consistent scoring ability and his durability in the NBA. The record, which began in January 2007, reached 867 consecutive games, highlighting LeBron’s remarkable resilience and his capacity to perform at a high level night after night. This milestone underscored his place among the greatest scorers in NBA history and demonstrated his unwavering commitment to excellence over a sustained period." },
    { year: "2021", lebron: "Featured in Space Jam 2", jordan: "", funfact: "" },
    { year: "2023", lebron: "LeBron becomes NBA’s all-time leading scorer", jordan: "", funfact: "In 2023, LeBron James reached the pinnacle of individual scoring achievement by becoming the NBA's all-time leading scorer, surpassing Kareem Abdul-Jabbar’s record of 38,387 points. This historic milestone encapsulated LeBron’s extraordinary career, marked by his versatility, longevity, and scoring prowess. Achieving this record was a testament to his adaptability and sustained excellence over two decades, solidifying his legacy as one of the greatest basketball players ever. This moment not only highlighted his scoring capabilities but also his overall impact on the game and his ability to remain at the top of his profession for an extended period." }
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

  let scrolled = false;

  window.addEventListener('scroll', function() {
    // Check if the user has scrolled to a specific point
    if (!scrolled && window.scrollY > 500) { // Adjust 500 to the desired scroll position
      startMarqueeAnimation(); // Call the function to start the animation
      scrolled = true; // Set scrolled to true to prevent the animation from restarting
    }
  });

  function startMarqueeAnimation() {
    // Apply animation to the marquee line
    document.querySelector('.marquee-line').style.animation = 'marquee-line 2s linear infinite';
  }
</script>

<p>Now, let's take a journey through the years to explore some of the milestone achievements of 
  LeBron James and Michael Jordan. Hover over the basketballs outlined in yellow to discover more!</p>
  <br><br>


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
<br><br><br><br><br><br><br><br><br><br><br><br><br><br>
<p>The debate will continue, but one thing remains clear: both Jordan and LeBron have cemented their places in basketball history, each in their unique and legendary ways. Your choice depends on what you value most in a player, and that's what makes this debate so captivating. But, now that we have reached the end of their game... <br><br></p>
<h2>  Who do you think is the NBA GOAT? </h2>

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
  
  h2 {
  text-align: center; 
  max-width: 700px; 
  margin: 0 auto; 
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

