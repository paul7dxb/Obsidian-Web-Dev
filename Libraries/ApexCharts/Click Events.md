```JS
const StackedBarYear = (props) => {
	const barChartSeries = props.barChartSeries;
	const barChartLabels = props.barChartLabels;

	const horizChartOptions = {
		chart: {
			type: "bar",
			height: 350,
			stacked: true,
			events: {
				click: function (event, chartContext, config) {
					// The last parameter config contains additional information like `seriesIndex` and `dataPointIndex` for cartesian charts
					console.log("event");
					console.log(event);
					console.log("chartContext");
					console.log(event.explicitOriginalTarget.data);
				},
			},
			xAxisLabelClick: function (event, chartContext, config) {
				console.log("xaxis click");
			},
			dataPointSelection: function(event, chartContext, config) {        
				console.log("Index row of data")
				console.log(config.dataPointIndex)
				console.log("Index of dataset (Stan=cked Bar chart)")
				console.log(config.seriesIndex)
				console.log(barChartSeries[config.seriesIndex].name)
			}
```