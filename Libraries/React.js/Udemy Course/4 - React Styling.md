# Style Prop

- Same as usual HTML one
- Wants a JS object
	- So use double curly brace {{}}
	- CSS keyname
	- Value as value
- If property contains '-' then either put quotes around property, or use camel case property
	- backgroundColor

# Setting Property Inline

- Overrides all CSS values

```jsx
<div className="chart-bar__fill" style={{ height: barFillHeight }}></div>
```

Inline conditional with ternary operator

```jsx
const [isValid, setIsValid] = useState(true);
...

<label style={{color : !isValid ? 'red' : 'black'}} >Course Goal</label>
```

# Setting CSS Classes Dynamilly

- [Udemy Lecture](https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/25597258#overview)
- [[JS#Template Literal]]

```jsx
<div className={`form-control ${!isValid ? 'invalid' : ''}`}>
```

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

# Scope

- Avoiding CSS clashes

## Styled Components Package

## Install

- Install into node modules folder
```bash
npm install --save styled-components
```

- Potenital VSCode extension for nicer CSS between ticks - jpoissonnier.vscode-styled-components

## Usage

- Create constant in component with CSS in [[JS#Template Literal|template literal]]
- Pseudo selectors replace element with `&`
	- `button:hover` becomes `&:hover`

Without styled components:
CSS
```css
.button {
  font: inherit;
  padding: 0.5rem 1.5rem;
  border: 1px solid #8b005d;
  color: white;
  background: #8b005d;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
  cursor: pointer;
}

.button:focus {
  outline: none;
}

.button:hover,
.button:active {
  background: #ac0e77;
  border-color: #ac0e77;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
}

```

JSX
```jsx
const Button = props => {
  return (
    <button className="button">
      {props.title}
    </button>
  );
};

export default Button;
```

With styled components:
```JS
import styled from "styled-components";

const Button = styled.button`
  font: inherit;
  padding: 0.5rem 1.5rem;
  border: 1px solid #8b005d;
  color: white;
  background: #8b005d;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
  cursor: pointer;

  &:focus {
    outline: none;
  }

  &:hover,
  &:active {
    background: #ac0e77;
    border-color: #ac0e77;
    box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
  }
`;

export default Button;
```

Add props class to styled component
Another example:

```jsx
import styled from "styled-components";

const FormControl = styled.div`
  margin: 0.5rem 0;

  & label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
  }

  & input {
    display: block;
    width: 100%;
    border: 1px solid #ccc;
    font: inherit;
    line-height: 1.5rem;
    padding: 0 0.25rem;
  }

  & input:focus {
    outline: none;
    background: #fad0ec;
    border-color: #8b005d;
  }

  &.invalid input{
    border-color: red;
    background-color: rgb(227, 186, 186);
    border-width: 1px;
    border-style: solid;
  }

  &.invalid label
    background-color: red;
  }
`;

...

<FormControl className={!isValid ? "invalid" : ""}>
<label>Course Goal</label>
<input type="text" onChange={goalInputChangeHandler} />
</FormControl>


```

Or use props inside the styled componets ticks using `${}` and an arrow function

```JSX
import styled from "styled-components";

const FormControl = styled.div`
  margin: 0.5rem 0;

  & label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
    color: ${props => props.invalid ? "red" : 'black'};

  }

  & input {
    display: block;
    width: 100%;
    border: 1px solid ${props => props.invalid ? "red" : '#ccc'};
    background: ${props => props.invalid ? "#ffd7d7" : 'transparent'};
    font: inherit;
    line-height: 1.5rem;
    padding: 0 0.25rem;
  }

  & input:focus {
    outline: none;
    background: #fad0ec;
    border-color: #8b005d;
  }

`;

...

  <FormControl invalid={!isValid}>
	<label>Course Goal</label>
	<input type="text" onChange={goalInputChangeHandler} />
  </FormControl>
```