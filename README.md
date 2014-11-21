Chart.LogarithmicLine.js
===================

*LogarithmicLine plugin for Chart.js* [chartjs.org](http://www.chartjs.org)

## Usage

### Introduction
A line chart with logarithmic y-axis is a way of showing data with a high value range.


### Example usage
```javascript
var myLogarithmicLineChart = new Chart(ctx).LogarithmicLine(data, options);
```

### Data structure

```javascript
var data = {
  labels: ["January", "February", "March", "April", "May", "June", "July"],
  datasets: [
  {
    label: "My First dataset",
    fillColor: "rgba(220,220,220,0.5)",
    strokeColor: "rgba(220,220,220,0.8)",
    highlightFill: "rgba(220,220,220,0.75)",
    highlightStroke: "rgba(220,220,220,1)",
    data: [1, 15, 96, 150, 600, 5000, 9000]
  },
  {
    label: "My Second dataset",
    fillColor: "rgba(151,187,205,0.5)",
    strokeColor: "rgba(151,187,205,0.8)",
    highlightFill: "rgba(151,187,205,0.75)",
    highlightStroke: "rgba(151,187,205,1)",
    data: [120, 9, 65, 300, 700, 1200, 900]
  }
  ]
};
```

### Chart Options

These are the customisation options specific to LogarithmicLine charts.

```javascript
{

  ///Boolean - Whether grid lines are shown across the chart
  scaleShowGridLines : true,

  //String - Colour of the grid lines
  scaleGridLineColor : "rgba(0,0,0,.05)",

  //Number - Width of the grid lines
  scaleGridLineWidth : 1,

  //Boolean - Whether the line is curved between points
  bezierCurve : true,

  //Number - Tension of the bezier curve between points
  bezierCurveTension : 0.4,

  //Boolean - Whether to show a dot for each point
  pointDot : true,

  //Number - Radius of each point dot in pixels
  pointDotRadius : 4,

  //Number - Pixel width of point dot stroke
  pointDotStrokeWidth : 1,

  //Number - amount extra to add to the radius to cater for hit detection outside the drawn point
  pointHitDetectionRadius : 20,

  //Boolean - Whether to show a stroke for datasets
  datasetStroke : true,

  //Number - Pixel width of dataset stroke
  datasetStrokeWidth : 2,

  //Boolean - Whether to fill the dataset with a colour
  datasetFill : true,

  //String - A legend template
  legendTemplate : "<ul class=\"<%=name.toLowerCase()%>-legend\"><% for (var i=0; i<datasets.length; i++){%><li><span style=\"background-color:<%=datasets[i].strokeColor%>\"></span><%if(datasets[i].label){%><%=datasets[i].label%><%}%></li><%}%></ul>"

}
```

You can override these for your `Chart` instance by passing a second argument into the `LogarithmicLine` method as an object with the keys you want to override.

For example, we could have a logarithmic line chart without a stroke on each dataset by doing the following:

```javascript
new Chart(ctx).LogarithmicLine(data, {
  datasetStroke: false
  });
  // This will create a chart with all of the default options, merged from the global config,
  //  and the LogarithmicLine chart defaults but this particular instance will have `datasetStroke` set to false.
  ```

  We can also change these defaults values for each LogarithmicLine type that is created, this object is available at `Chart.defaults.LogarithmicLine`.

### Prototype methods

#### .getPointsAtEvent( event )

  Calling `getPointsAtEvent(event)` on your Chart instance passing an argument of an event, or jQuery event, will return the point elements that are at that the same position of that event.

  ```javascript
  canvas.onclick = function(evt){
    var activePoints = myLogarithmicLineChart.getPointsAtEvent(evt);
    // => activePoints is an array of points on the canvas that are at the same position as the click event.
  };
  ```

  This functionality may be useful for implementing DOM based tooltips, or triggering custom behaviour in your application.

#### .update( )

  Calling `update()` on your Chart instance will re-render the chart with any updated values, allowing you to edit the value of multiple existing points, then render those in one animated render loop.

  ```javascript
  myLogarithmicLineChart.datasets[0].lines[2].value = 50;
  // Would update the first dataset's value of 'March' to be 50
  myLogarithmicLineChart.update();
  // Calling update now animates the position of March from 96 to 50.
  ```

#### .addData( valuesArray, label )

  Calling `addData(valuesArray, label)` on your Chart instance passing an array of values for each dataset, along with a label for those lines.

  ```javascript
  // The values array passed into addData should be one for each dataset in the chart
  myLogarithmicLineChart.addData([40, 60], "August");
  // The new data will now animate at the end of the chart.
  ```

  #### .removeData( )

  Calling `removeData()` on your Chart instance will remove the first value for all datasets on the chart.

  ```javascript
  myLogarithmicLineChart.removeData();
  // The chart will now animate and remove the first point
  ```

## License

Chart.LogarithmicLine.js is available under the [MIT license](http://opensource.org/licenses/MIT).

## Bugs & issues

When reporting bugs or issues, if you could include a link to a simple [jsbin](http://jsbin.com) or similar demonstrating the issue, that'd be really helpful.
