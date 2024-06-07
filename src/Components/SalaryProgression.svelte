<script>
    import { onMount } from 'svelte';
    import { salaryData } from '../../data/salaries.js';
    import { realSalaryData } from '../../data/real_salaries.js';
    import * as d3 from 'd3';

    let svg;
    let tooltip;

    onMount(() => {
        const margin = {
            top: 70,
            bottom: 80,
            left: 150,
            right: 90,
        };
        const width = 800 - margin.left - margin.right;
        const height = 600 - margin.top - margin.bottom;

        const svgElement = d3.select(svg)
            .attr("width", width + margin.left + margin.right)
            .attr("height", height + margin.top + margin.bottom)
            .append("g")
            .attr("transform", `translate(${margin.left},${margin.top})`);

        const tooltipElement = d3.select(tooltip);

        const parseSalary = d => +d.Salary.replace(/\$|,/g, '');
        const parseSeason = d => d.Season;

        const dataMJ = realSalaryData.filter(d => d.Player === "Michael Jordan").map(d => {
            const original = salaryData.find(s => s.Season === d.Season && s.Player === "Michael Jordan");
            return {
                season: parseSeason(d),
                salary: parseSalary(original),
                realSalary: parseSalary(d)
            };
        });

        const dataLBJ = realSalaryData.filter(d => d.Player === "Lebron James").map(d => {
            const original = salaryData.find(s => s.Season === d.Season && s.Player === "Lebron James");
            return {
                season: parseSeason(d),
                salary: parseSalary(original),
                realSalary: parseSalary(d)
            };
        });

        const allSeasons = [...new Set([...dataMJ, ...dataLBJ].map(d => d.season))];
        const x = d3.scalePoint()
            .domain(allSeasons)
            .range([0, width])
            .padding(0.5);

        const y = d3.scaleLinear()
            .domain([0, d3.max([...dataMJ, ...dataLBJ], d => d.realSalary)])
            .nice()
            .range([height, 0]);

        const lineMJ = d3.line()
            .x(d => x(d.season))
            .y(d => y(d.realSalary))
            .curve(d3.curveLinear);

        const lineLBJ = d3.line()
            .x(d => x(d.season))
            .y(d => y(d.realSalary))
            .curve(d3.curveLinear);

        // Draw the x and y axes
        svgElement.append("g")
            .attr("transform", `translate(0,${height})`)
            .call(d3.axisBottom(x).tickSize(0))
            .selectAll("text")
            .style("text-anchor", "end")
            .attr("dx", "-.8em")
            .attr("dy", ".15em")
            .attr("transform", "rotate(-65)");

        svgElement.append("g")
            .call(d3.axisLeft(y));

        // Draw the lines
        svgElement.append("path")
            .datum(dataMJ)
            .attr("class", "line")
            .attr("fill", "none")
            .attr("stroke", "#A62929")
            .attr("d", lineMJ);

        svgElement.append("path")
            .datum(dataLBJ)
            .attr("class", "line")
            .attr("fill", "none")
            .attr("stroke", "#00008B")
            .attr("d", lineLBJ);

        const handleMouseOver = (event, d) => {
            tooltipElement.style("visibility", "visible")
                .html(`Season: ${d.season} <br> Salary (after inflation): $${d.realSalary.toLocaleString()} <br> Salary (before inflation): $${d.salary.toLocaleString()}`);
        };

        const handleMouseMove = (event) => {
            tooltipElement.style("top", `${event.pageY - 10}px`)
                .style("left", `${event.pageX + 10}px`);
        };

        const handleMouseOut = () => {
            tooltipElement.style("visibility", "hidden");
        };

        svgElement.selectAll(".dotMJ")
            .data(dataMJ)
            .enter().append("circle")
            .attr("class", "dotMJ")
            .attr("cx", d => x(d.season))
            .attr("cy", d => y(d.realSalary))
            .attr("r", 4)
            .attr("fill", "#A62929")
            .on("mouseover", handleMouseOver)
            .on("mousemove", handleMouseMove)
            .on("mouseout", handleMouseOut);

        svgElement.selectAll(".dotLBJ")
            .data(dataLBJ)
            .enter().append("circle")
            .attr("class", "dotLBJ")
            .attr("cx", d => x(d.season))
            .attr("cy", d => y(d.realSalary))
            .attr("r", 4)
            .attr("fill", "#00008B")
            .on("mouseover", handleMouseOver)
            .on("mousemove", handleMouseMove)
            .on("mouseout", handleMouseOut);

        // Axis labels
        svgElement.append("text")
            .attr("class", "axis-label")
            .attr("y", height + margin.bottom - 35)
            .attr("x", (width) / 2)
            .attr("text-anchor", "middle")
            .text("Season");

        svgElement.append("text")
            .attr("class", "axis-label")
            .attr("y", -(margin.left / 3) - 45)
            .attr("x", -(height / 2))
            .attr("text-anchor", "middle")
            .attr("transform", "rotate(-90)")
            .text("Salary ($)");
    });
</script>

<p class="p-left">
    One of the key components in the debate is their salary. we have adjusted it for inflation:
</p>

<div class="chart-container">
    <svg bind:this={svg} id="salary-chart"></svg>
    <div bind:this={tooltip} class="tooltip"></div>
</div>

<p class="p-left">
    We can see that Jordan's salary has had 2 very steep changes, one from season 11 to season 12, the other from season 13 to season 14. Season 11 was the end of his 8-year contract, which also ended the year he won a championship. In that year, the Knicks offered him a ludicrous amount of money, and to keep Jordan on the team, the Bulls offered him $30 million dollars a year. In season 14, he returned to basketball after retiring. He played for the Washington Wizards, a team he part-owned. Jordan took a lower salary to help with the team's salary cap.<br><br>
    When we trace the blue line, we can see that James' salary is consistently increasing. From the 6th season to the 7th season, we can see that James' salary went down. This is the year he switched from the Miami Heat to the Cleveland Cavaliers. Another thing to note is the salary increase from season 12 to season 13. After James' won the NBA Finals with the Cavaliers in season 12, his salary increased by $8 million.
</p>
<p>
"Who do you think won this round?"</p>

<style>
    .chart-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 100%;
    }
    .chart-container p {
        max-width: 600px;
        margin: 1rem auto;
        padding-top: 3rem;
    }
    #salary-chart {
        margin: auto;
        width: 50%;
        margin: 1rem auto;
        padding-left: 78px;
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

    p {
  text-align: center; 
  max-width: 700px; 
  margin: 0 auto; 
  padding-top: 50px;
}

.p-left {
  text-align: left;
}
</style>
