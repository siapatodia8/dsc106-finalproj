<script>
  import katexify from "../katexify";
  import { select, selectAll } from "d3-selection";
</script>

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

<section>
  <div class="section-container">
    <div class="image-container">
      <h1 class='step-title'>LeBron James</h1>
      <img id="chart2" src="https://www.freeiconspng.com/thumbs/lebron-james-png/lebron-james-png-8.png" alt="LeBron James image">
    </div>
    <div class="text-container">
      <br><br><br>
      <h1 class='step-title'></h1>
      <br>
      <p>In recent years, James has been in the conversation for the greatest basketball player ever. As of 2024,
        James has played for 21 years and won 4 of the 10 finals he made. Amongst elite NBA players, LeBron has had
        one of the longest careers, with the longest being Vince Carter’s career lasting 22 years. </p>
      <br><br>
      <p>While some people value Jordan’s 3-peats and 6 NBA rings, others value James’ longevity and his consistent high level
        of performance across all 21 years, with an average of 27.1 points per game. In those 21 years, his worst year was an
        impressive 20 points per game in his rookie season, and his best year was 31.4 points per game in his 2005-06 season. 
      </p>
      <br><br>
      <p>In recent years, James has been in the conversation for the greatest basketball player ever. As of 2024,
        James has played for 21 years and won 4 of the 10 finals he made. Amongst elite NBA players, LeBron has had
        one of the longest careers, with the longest being Vince Carter’s career lasting 22 years. </p>
      <br><br>
      <p>While some people value Jordan’s 3-peats and 6 NBA rings, others value James’ longevity and his consistent high level
        of performance across all 21 years, with an average of 27.1 points per game. In those 21 years
      </p>
    </div>
    <div class="image-container">
      <h1 class='step-title'>Michael Jordan</h1>
      <img id="chart3" src="https://www.pngall.com/wp-content/uploads/5/Michael-Jordan-Basketball-Player-Transparent.png" alt="Michael Jordan image">
    </div>
  </div>
  <br /><br />
  <p class="body-text"></p>
</section>

<style>
  .header-section {
    text-align: center;
    margin-bottom: 2rem;
  }

  .name-container {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 70rem;
  }

  .player {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .player-name {
    /* font-family: 'Montserrat', sans-serif; */
    font-size: 3rem;
    font-weight: 550;
    margin-bottom: 1rem;
    color: #333333;
  }

  .image-container img {
    width: 100%;
    max-width: 1000px;
    display: block;
    margin: 1rem 0;
    opacity: 0.8;
  }

  .section-container {
    margin-top: 0em;
    text-align: center;
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
  }

  .step-title {
    /* font-family: 'Montserrat', sans-serif; */
    font-size: 3rem;
    font-weight: 550;
    margin-bottom: 1rem;
    color: #333333;
    text-align: center;
  }

  .text-container {
    font-size: 18px;
    background: var(--bg);
    color: #000000;
    padding: 0.5rem 1rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: left;
    width: 75%;
    margin: auto;
    max-width: 700px;
    font-family: var(--font-main);
  }

  .image-container {
    flex: 1 1 20%;
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

    .text-container {
      width: 95%;
      max-width: 768px;
      font-size: 17px;
      line-height: 1.6;
    }

    .image-container img {
      max-width: 150px;
    }
  }

  p {
  text-align: center; 
  max-width: 700px; 
  margin: 0 auto; 
}

/* .p-left {
  text-align: left;
} */
</style>


