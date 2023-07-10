- My Github hosted images
	- https://paul7dxb.github.io/hosted-assets/

# Useful Websites

- webhook testing
	- https://www.piesocket.com/websocket-tester


```js
const result = response.json() // array of stopPoints

const stopPoints = result.stopPoints

stopPoints.sort( (stopPointA, stopPointB) => stopPointA.distance - stopPointB.distance)

return stopPoints.map( (stopPoint) => {
	return {id: stopPoint.naptanId, distance : stopPoint.distance}
})

// distance

// sort predictionA.timeToStation - predictionB.timeToStation
// stationName, lineName, destinationName, timeToStation

//date fns
// intlFormatDistance // relative date comparison

//format Duration
// secondsToMinutes

ha1 1qa

			destinationName: stopPoint.destinationName,
			timeToStation: stopPoint.timeToStation,

```