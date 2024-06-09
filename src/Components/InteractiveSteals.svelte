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
        SPG: +d.SPG // Changed from MP to SPG
      }));

      const averageSPG = d3.mean(processData, d => d.SPG); // Changed from MP to SPG

      const x = d3.scaleBand()
        .range([0, 2 * Math.PI])
        .align(0)
        .domain(processData.map(d => d.SEASON));

      const y = d3.scaleRadial()
        .range([innerRadius, outerRadius])
        .domain([0, d3.max(processData, d => d.SPG)]); // Changed from MP to SPG

      svg.append("g")
        .selectAll("path")
        .data(processData)
        .enter()
        .append("path")
        .attr("fill", color)
        .attr("d", d3.arc()
          .innerRadius(innerRadius)
          .outerRadius(d => y(d.SPG)) // Changed from MP to SPG
          .startAngle(d => x(d.SEASON))
          .endAngle(d => x(d.SEASON) + x.bandwidth())
          .padAngle(0.01)
          .padRadius(innerRadius))
        .on("mouseover", (event, d) => {
          tooltip.style("visibility", "visible")
            .text(`${d.SEASON}: ${d.SPG}`); // Changed from MP to SPG
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
        .attr("transform", d => `rotate(${(x(d.SEASON) + x.bandwidth() / 2) * 180 / Math.PI - 90})translate(${y(d.SPG) + 10},0)`) // Changed from MP to SPG
        .append("text")
        .text(d => d.SEASON)
        .attr("transform", d => (x(d.SEASON) + x.bandwidth() / 2 + Math.PI) % (2 * Math.PI) < Math.PI ? "rotate(180)" : "rotate(0)")
        .style("font-size", "11px")
        .attr("alignment-baseline", "middle");


    svg.append("text")
        .text(`Avg: ${averageSPG.toFixed(2)}`) // Changed from MP to SPG
        .attr("text-anchor", "middle")
        .attr("dy", "0.35em")
        .style("font-size", "14px")
        .style("fill", color);

  };

    createChart(MJ_data, mjSvgElement, "#A62929");
    createChart(LBJ_data, lbjSvgElement, "#00008B");
  });
</script>


<div class="chart-container">
  <div class="chart-wrapper">
    <div class="chart">
      <svg bind:this={lbjSvgElement}></svg>
    </div>
    <div class="textbox">
      <h1>Steals Per Game</h1>
      <p>With more steals per game, Jordan seems to be more agile and have higher basketball IQ. Stealing a ball 
      requires reading the opponent and positional awareness. Jordan seems to assist his team more on defense.</p>
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
  font-size: 28px;
  font-weight: bold;
}

.textbox p {
  font-size: 24px;
}

</style>

