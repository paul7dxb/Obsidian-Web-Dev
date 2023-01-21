# Style Prop

- Same as usual HTML one
- Wants a JS object
	- So use double curly brace {{}}
	- CSS keyname
	- Value as value
- If property contains '-' then either put quotes around property, or use camel case property
	- backgroundColor



# Examples

## Example: Percentage fill by Dynamic Value

- See Chart in [Udemy Example Project Expenses](https://github.com/academind/react-complete-guide-code/tree/05-rendering-lists-conditional-content/code/06-finished/src)

ExpensesChart.js:
- Collect the data to display

```JSX
import React from "react";
import Chart from "../Chart/Chart";

const ExpensesChart = (props) => {
    const chartDataPoints = [
        { label: 'Jan', value: 0},
        { label: 'Feb', value: 0},
        { label: 'Mar', value: 0},
        { label: 'Apr', value: 0},
        { label: 'May', value: 0},
        { label: 'Jun', value: 0},
        { label: 'Jul', value: 0},
        { label: 'Aug', value: 0},
        { label: 'Sep', value: 0},
        { label: 'Oct', value: 0},
        { label: 'Nov', value: 0},
        { label: 'Dec', value: 0}
    ];

    for (const expense of props.expenses){
        const expenseMonth = expense.date.getMonth(); //Starts at Jan = 0. Same as indexes of array
        chartDataPoints[expenseMonth].value += expense.amount;
    }

    return(
        <Chart dataPoints={chartDataPoints} />
    )
}

export default ExpensesChart;
```

Chart.js:
Process data and assign to component to display
```JSX
import "./Chart.css";
import ChartBar from "./ChartBar";

const Chart = (props) => {

    const dataPointValues = props.dataPoints.map(dataPoint => dataPoint.value)
    const totalMaximum = Math.max(...dataPointValues);

  return (
    <div className="chart">
      {props.dataPoints.map((dataPoint) => (
        <ChartBar
          key={dataPoint.label}
          value={dataPoint.value}
          maxValue={totalMaximum}
          label={dataPoint.label}
        />
      ))}
    </div>
  );
};

export default Chart;
```

ChartBar.js
- Perform calculations for CSS properties
- Assign CSS properties using [[#Style Prop]]

```JSX
import React from "react";
import "./ChartBar.css";

const ChartBar = (props) => {
  let barFillHeight = "0%";
  if (props.maxValue > 0) {
    barFillHeight = Math.round((props.value / props.maxValue) * 100) + "%"; 
}

  return (
    <div className="chart-bar">
      <div className="chart-bar__inner">
        <div className="chart-bar__fill" style={{ height: barFillHeight }}></div>
      </div>
      <div className="chart-bar__label">{props.label}</div>
    </div>
  );
};

export default ChartBar;
```