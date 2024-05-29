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
            innerRadius = 90,
            outerRadius = Math.min(width, height) / 2;
  
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
      };
  
      createChart(MJ_data, mjSvgElement, "#A62929");
      createChart(LBJ_data, lbjSvgElement, "#00008B");
    });
  </script>
  

  <div class="chart-container">
    <h1 class="body-header">Interactive Chart Example</h1>
    <div class="chart-wrapper">
      <div class="chart">
        <h1>Michael Jordan Points Per Game</h1>
        <svg bind:this={mjSvgElement}></svg>
      </div>
      <div class="chart">
        <h1>LeBron James Points Per Game</h1>
        <svg bind:this={lbjSvgElement}></svg>
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

  </style>