### 넥사크로의 WebBrowser 컴포넌트를 이용하여 차트가 구현된 html 페이지를 호출하여 차트를 연동 합니다.

```swift
var strUrl = “http://www.xplatform.co.kr:8080/Next_JSP/GoogleChart/chart/Area.html “;
this.WebBrowser00.set_url(strUrl);

 

<html>
<head>
   <script type=“text/javascript” src=“https://www.gstatic.com/charts/loader.js”></script>
   <script type=“text/javascript”>
     google.charts.load(‘current’, {‘packages’:['corechart']});
     google.charts.setOnLoadCallback(drawChart);
   var data;
   var option;
   var chart;
     function drawChart() {
      data = google.visualization.arrayToDataTable([
       ['Year', 'Sales', 'Expenses'],
       ['2013', 1000, 400],
       ['2014', 1170, 460],
       ['2015', 660, 1120],
       ['2016', 1030, 540]
     ]);
     options = {
      title: ‘Company Performance’,
      hAxis: {title: ‘Year’, titleTextStyle: {color: ‘#333′}},
      vAxis: {minValue: 0}
     };
     chart = new google.visualization.AreaChart(document.getElementById(‘chart_div’));
     chart.draw(data, options);
   }   function btnCallChart(argData, argOption) {
     for(var i=0; i<data.getNumberOfColumns(); i++) {
      data.setColumnLabel(i, argData[0][i]);
      }
      for(var i=0; i<data.getNumberOfRows(); i++) {
      for(var j=0; j<data.getNumberOfColumns(); j++) {
      data.setValue(i, j, argData[i+1][j]);
       }
      }
      options = {
       title: argOption[0],
       hAxis: argOption[1],
       vAxis: argOption[2],
      };
      chart.draw(data, options);
   }
   </script>
</head>
<body>
   <div id=”chart_div” style=”width: 100%; height: 100%;”></div>
</body>
</html>
 

*차트 표현은 json data 포맷으로 데이터를 만들어 연동 합니다.
[['Task', 'Hours per Day'],['Work',2],['Eat',2],['Commute', 11],['Watch TV', 2],['Sleep',7]]

*WebBrowser 컴포넌트에 호출된 html에 아래와 같이 값을 넘겨 주게 됩니다.
var arrData = eval(this.DsChart.getColumn(nRow,”data”));
var arrOption = eval(this.DsChart.getColumn(nRow,”opt”));
this.WebBrowser00.callMethod(“btnCallChart”,arrData,arrOption);

```

[주의사항]
구글 차트는 SVG (Scalable Vector Graphics), VML(Vector Markup Language) 기능을 사용하기때문에 브라우저에 따라 사용이 되지 않을 수 있습니다.

[SVG지원 브라우저 사양]
Internet Explorer : IE9부터 SVG를 지원
Opera : 8.0 Beta3 부터 SVG 1.1 Tiny를 지원
Firefox : 1.5 베타 1 이후 지원
Safari : SVG를 지원하지 않음

[참고사이트]
Documentation : https://developers.google.com/chart/interactive/docs
