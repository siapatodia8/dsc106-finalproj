<script>
  import { onMount } from 'svelte';
  import MJ_data from '../../data/MJ_yearly_stats.js';
  import LBJ_data from '../../data/LBJ_yearly_stats.js';
  import * as d3 from 'd3';

  let mjSvgElement;
  let lbjSvgElement;
  let tooltipElement;

  onMount(() => {
    const margin = { top: 50, right: 0, bottom: 80, left: 0 },
          width = 500 - margin.left - margin.right,
          height = 500 - margin.top - margin.bottom,
          innerRadius = 60,
          outerRadius = Math.min(width, height) / 2 - 30;

    const createChart = (data, svgElement, color) => {
      const svg = d3.select(svgElement)
        .attr("width", width + margin.left + margin.right)
        .attr("height", height + margin.top + margin.bottom)
        .append("g")
        .attr("transform", `translate(${(width / 2) + margin.left}, ${(height / 2) + margin.top})`);

      const tooltip = d3.select(tooltipElement)
        .style("position", "absolute")
        .style("visibility", "hidden")
        .style("background", "rgba(0, 0, 0, 0.7)")
        .style("color", "#fff")
        .style("padding", "5px")
        .style("border-radius", "5px")
        .style("font-size", "12px");

      const processData = data.map(d => ({
        SEASON: d.SEASON,
        PPG: +d.PPG
      }));

      const averagePPG = d3.mean(processData, d => d.PPG);

      const x = d3.scaleBand()
        .range([0, 2 * Math.PI])
        .align(0)
        .domain(processData.map(d => d.SEASON));

      const y = d3.scaleRadial()
        .range([innerRadius, outerRadius])
        .domain([0, d3.max(processData, d => d.PPG)]);

      svg.append("g")
        .selectAll("path")
        .data(processData)
        .enter()
        .append("path")
        .attr("fill", color)
        .attr("d", d3.arc()
          .innerRadius(innerRadius)
          .outerRadius(d => y(d.PPG))
          .startAngle(d => x(d.SEASON))
          .endAngle(d => x(d.SEASON) + x.bandwidth())
          .padAngle(0.01)
          .padRadius(innerRadius))
        .on("mouseover", (event, d) => {
          tooltip.style("visibility", "visible")
            .text(`${d.SEASON}: ${d.PPG}`);
        })
        .on("mousemove", event => {
          tooltip.style("top", (event.pageY - 10) + "px")
            .style("left", (event.pageX + 10) + "px");
        })
        .on("mouseout", () => {
          tooltip.style("visibility", "hidden");
        });

      svg.append("g")
        .selectAll("g")
        .data(processData)
        .enter()
        .append("g")
        .attr("text-anchor", d => (x(d.SEASON) + x.bandwidth() / 2 + Math.PI) % (2 * Math.PI) < Math.PI ? "end" : "start")
        .attr("transform", d => `rotate(${(x(d.SEASON) + x.bandwidth() / 2) * 180 / Math.PI - 90})translate(${y(d.PPG) + 10},0)`)
        .append("text")
        .text(d => d.SEASON)
        .attr("transform", d => (x(d.SEASON) + x.bandwidth() / 2 + Math.PI) % (2 * Math.PI) < Math.PI ? "rotate(180)" : "rotate(0)")
        .style("font-size", "11px")
        .attr("alignment-baseline", "middle");


    svg.append("text")
        .text(`Avg: ${averagePPG.toFixed(2)}`)
        .attr("text-anchor", "middle")
        .attr("dy", "0.35em")
        .style("font-size", "14px")
        .style("fill", color);

  };

    createChart(LBJ_data, lbjSvgElement, "#00008B");
    createChart(MJ_data, mjSvgElement, "#A62929");
    
  });
</script>

<div class="intro-paragraph">
  <p></p>
</div>

<div class="chart-container">
  <div class="chart-wrapper">
    <div class="chart">
      <svg bind:this={lbjSvgElement}></svg>
    </div>
    <div class="textbox">
      <h1>Points Per Game
        </h1>
      <p>Average points per game (PPG) per season is a crucial statistic for evaluating NBA players as it directly measures their scoring ability, highlighting their offensive impact and consistency over time.
         High PPG indicates a player's role as a primary scoring option and their reliability in generating points for the team.<br><br>
        </p>
    </div>
    <div class="chart">
      <svg bind:this={mjSvgElement}></svg>
    </div>
  </div>
  <div bind:this={tooltipElement}></div>
</div>


<style>
  .chart-container {
    text-align: center;
  }
  svg {
    display: block;
    margin: auto;
  }
  .chart-wrapper {
  display: flex;
  justify-content: space-around;
  }

  .chart {
  flex: 1;
  text-align: center;
  margin: 0 10px;
  }

  svg {
  display: block;
  margin: auto;
  }

.textbox {
  display: inline-block;
  background-color: rgba(221, 221, 221, 0.3); 
  /* border: 2px solid #000000;  */
  padding: 20px; 
  width: 650px;
  height: 300px;
  position: relative;
  top: 80px;
}

.textbox h1 {
  font-size: 24px;
  font-weight: bold;
}

.textbox p {
  font-size: 14px;
  position: center;
}

.intro-paragraph {
  text-align: center; 
  margin-bottom: 20px; /* Add some space between the intro paragraph and the chart container */
}
</style>
