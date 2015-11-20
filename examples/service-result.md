---
layout: example
title: Presentation Demo
usedxchart: true
---

<div id="chartContainer" style="width:500px;height:0px"></div>

{% capture survey_setup %}
var survey = new Survey.Survey({
        surveyId: '5af48e08-a0a5-44a5-83f4-1c90e8e98de1',
        surveyPostId: '3ce10f8b-2d8a-4ca2-a110-2994b9e697a1'
});

survey.onSendResult.add(function(s, options) {
    if(options.success) {
        s.getResult('a15eee7a-9418-4eb4-9671-2009c8ff6b24', 'langs');
    }
});
survey.onGetResult.add(function(s, options) {
    if(options.success) {
        showChart(options.dataList);
    }
});
function showChart(chartDataSource) {
    document.getElementById("chartContainer").style.height = "500px";
    $("#chartContainer").dxPieChart({
        dataSource: chartDataSource,
        series: {
            argumentField: 'name',
            valueField: 'value'
        }
    });
}

{% endcapture %}
{% include live-example-code.html %}