<template>
  <div class="home">
    <div class="hello" ref="chartdiv">
  </div>
  </div>
</template>

<script>
import * as am4core from "@amcharts/amcharts4/core";
import * as am4charts from "@amcharts/amcharts4/charts";
import am4themes_animated from "@amcharts/amcharts4/themes/animated";

am4core.useTheme(am4themes_animated);

export default {
  name: 'Home',
  components: {

  },
  mounted() {
    let chart = am4core.create(this.$refs.chartdiv, am4charts.XYChart);

    chart.paddingRight = 20;

    let data = [];
    let visits = 10;
    for (let i = 1; i < 365; i++) {
      visits += Math.round((Math.random() < 0.5 ? 1 : -1) * Math.random() * 10);
      data.push({ date: new Date(2018, 0, i), name: "name" + i, value: visits });
    }



    var mockData = [
        {
            date: new Date('02-01-2020'),
            "cough": 1.4,
            "mucus": 1.5,
            "heavyBreathing": 2.8,
            "wheezing": 1.2
        },
        {
            date: new Date('02-08-2020'),
            "cough": 8.4,
            "mucus": 1.5,
            "heavyBreathing": 2.8,
            "wheezing": 1.2
        },
        {
            date: new Date('02-14-2020'),
            "cough": 0.4,
            "mucus": 2.5,
            "heavyBreathing": 2.8,
            "wheezing": 1.2
        },
        {
            date: new Date('02-21-2020'),
            "cough": 3.4,
            "mucus": 5.5,
            "heavyBreathing": 2.8,
            "wheezing": 1.2
        },
        {
            date: new Date('02-28-2020'),
            "cough": 5.4,
            "mucus": 4.5,
            "heavyBreathing": 2.8,
            "wheezing": 1.2
        },
        {
            date: new Date('03-01-2020'),
            "cough": 1.4,
            "mucus": 2.5,
            "heavyBreathing": 2.8,
            "wheezing": 1.2
        },
        {
            date: new Date('03-02-2020'),
            "cough": 4.4,
            "mucus": 3.5,
            "heavyBreathing": 2.8,
            "wheezing": 1.2
        },
        {
            date: new Date('03-10-2020'),
            "cough": 6.4,
            "mucus": 2.5,
            "heavyBreathing": 2.8,
            "wheezing": 1.2
        },
        {
            date: new Date('03-23-2020'),
            "cough": 1.4,
            "mucus": 1.5,
            "heavyBreathing": 2.8,
            "wheezing": 1.2
        },
        {
            date: new Date('03-13-2020'),
            "cough": 2.8,
            "mucus": 4.5,
            "heavyBreathing": 1.2,
            "wheezing": 2.2
        },
        {
            date: new Date('04-02-2020'),
            "cough": 5.2,
            "mucus": 1.5,
            "heavyBreathing": 6.8,
            "wheezing": 0.2
        },
    ]

    chart.data = mockData;

    console.log(chart.data)

    let dateAxis = chart.xAxes.push(new am4charts.DateAxis());
    dateAxis.renderer.grid.template.location = 0;
    dateAxis.zoomToDates(
      new Date('01-01-2020'),
      new Date()
    );

    let valueAxis = chart.yAxes.push(new am4charts.ValueAxis());
    valueAxis.tooltip.disabled = true;
    valueAxis.renderer.minWidth = 35;

    function createSeries(field, name, stacked) {
        var series = chart.series.push(new am4charts.ColumnSeries());
        series.dataFields.dateX = "date";
        series.dataFields.valueY = field;
        series.name = name;
        series.columns.template.tooltipText = "{name}: [bold]{valueY}[/]";
        series.stacked = stacked;
        series.columns.template.width = am4core.percent(75);

        var scrollbarX = new am4charts.XYChartScrollbar();
        scrollbarX.series.push(series);
        chart.scrollbarX = scrollbarX;
    }

    createSeries('cough', 'Cough', false);
    createSeries('mucus', 'Mucus', true);
    createSeries('heavyBreathing', 'Heavy Breathing', true);
    createSeries('wheezing', 'Wheezing', true);

    chart.cursor = new am4charts.XYCursor();



    this.chart = chart;

  },
  methods: {



  },

  beforeDestroy() {
    if (this.chart) {
      this.chart.dispose();
    }
  }

}
</script>

<style media="screen">
.hello {
    width: 100%;
    height: 500px;
    }
</style>
