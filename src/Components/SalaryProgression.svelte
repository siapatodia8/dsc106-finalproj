<script>
    import { salaryData } from '../../data/salaries.js';
    import * as d3 from 'd3';

    document.addEventListener('DOMContentLoaded', () => {
            const margin = {
                top: 70, 
                bottom: 80, 
                left: 100, 
                right: 50,
            };
            const width = 800 - margin.left - margin.right;
            const height = 600 - margin.top - margin.bottom;

            const svg = d3.select("#salary-chart")
                          .attr("width", width + margin.left + margin.right)
                          .attr("height", height + margin.top + margin.bottom)
                          .append("g")
                          .attr("transform", `translate(${margin.left},${margin.top})`);

            const tooltip = d3.select(".tooltip");

            const parseSalary = d => +d.Salary.replace(/\$|,/g, '');
            const parseSeason = d => d.Season;

            const dataMJ = salaryData.filter(d => d.Player === "Michael Jordan").map(d => ({
                season: parseSeason(d),
                salary: parseSalary(d)
            }));

            const dataLBJ = salaryData.filter(d => d.Player === "Lebron James").map(d => ({
                season: parseSeason(d),
                salary: parseSalary(d)
            }));

            const allSeasons = [...new Set([...dataMJ, ...dataLBJ].map(d => d.season))];
            const x = d3.scalePoint()
                        .domain(allSeasons)
                        .range([0, width])
                        .padding(0.5);

            const y = d3.scaleLinear()
                        .domain([0, d3.max([...dataMJ, ...dataLBJ], d => d.salary)])
                        .nice()
                        .range([height, 0]);

            const lineMJ = d3.line()
                 .x(d => x(d.season))
                 .y(d => y(d.salary))
                 .curve(d3.curveLinear);                    

            const lineLBJ = d3.line()
                  .x(d => x(d.season))
                  .y(d => y(d.salary))
                  .curve(d3.curveLinear);

            // Draw the x and y axes
            svg.append("g")
               .attr("transform", `translate(0,${height})`)
               .call(d3.axisBottom(x).tickSize(0))
               .selectAll("text")
               .style("text-anchor", "end")
               .attr("dx", "-.8em")
               .attr("dy", ".15em")
               .attr("transform", "rotate(-65)");

            svg.append("g")
               .call(d3.axisLeft(y));

            // Draw the lines
            svg.append("path")
                .datum(dataMJ)
                .attr("class", "line")
                .attr("fill", "none") 
                .attr("stroke", "#A62929")
                .attr("d", lineMJ);

                svg.append("path")
                .datum(dataLBJ)
                .attr("class", "line")
                .attr("fill", "none") 
                .attr("stroke", "#00008B")
                .attr("d", lineLBJ);

            const handleMouseOver = (event, d) => {
                tooltip.style("visibility", "visible")
                       .text(`Season: ${d.season} | Salary: $${d.salary.toLocaleString()}`);
            };

            const handleMouseMove = (event) => {
                tooltip.style("top", `${event.pageY - 10}px`)
                       .style("left", `${event.pageX + 10}px`);
            };

            const handleMouseOut = () => {
                tooltip.style("visibility", "hidden");
            };

            svg.selectAll(".dotMJ")
               .data(dataMJ)
               .enter().append("circle")
               .attr("class", "dotMJ")
               .attr("cx", d => x(d.season))
               .attr("cy", d => y(d.salary))
               .attr("r", 4)
               .attr("fill", "#A62929")
               .on("mouseover", handleMouseOver)
               .on("mousemove", handleMouseMove)
               .on("mouseout", handleMouseOut);

            svg.selectAll(".dotLBJ")
               .data(dataLBJ)
               .enter().append("circle")
               .attr("class", "dotLBJ")
               .attr("cx", d => x(d.season))
               .attr("cy", d => y(d.salary))
               .attr("r", 4)
               .attr("fill", "#00008B")
               .on("mouseover", handleMouseOver)
               .on("mousemove", handleMouseMove)
               .on("mouseout", handleMouseOut);

            // Axis labels
            svg.append("text")
            .attr("class", "axis-label")
            .attr("y", height + margin.bottom - 35) 
            .attr("x", (width) / 2)
            .attr("text-anchor", "middle")
            .text("Season");

            svg.append("text")
               .attr("class", "axis-label")
               .attr("y", -(margin.left/3)-45)
               .attr("x", -(height / 2))
               .attr("text-anchor", "middle")
               .attr("transform", "rotate(-90)")
               .text("Salary ($)");
        });

    </script>

<div class="chart-container">
    <h1>Salaries of Michael Jordan vs LeBron James</h1>
    <svg id="salary-chart"></svg>
    <div class="tooltip"></div>
</div>

<style>
    .chart-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 100%;
    }
    #salary-chart {
        margin: auto;
        max-height: 55vh;
        width: 50%;
        margin: 1rem auto;
    }

    .axis-text {
        font-size: 0.9rem;
    }

    .y-axis-line {
        opacity: 0.2;
    }

    .axis-label {
        text-transform: uppercase;
        font-size: 1rem;
    }

    .line {
        fill: none;
        stroke-linejoin: round;
        stroke-linecap: round;
        stroke-width: 3;
    }
    
    .tooltip {
        position: absolute;
        background: rgba(0, 0, 0, 0.7);
        color: #fff;
        padding: 5px;
        border-radius: 5px;
        font-size: 12px;
        visibility: hidden;
    }
</style>