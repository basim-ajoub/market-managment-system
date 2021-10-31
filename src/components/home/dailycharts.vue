<template>
    <div class="home-chart">
 <div id="chart">
        <apexchart id="area-chart" type="area" width="1010" height="290" :options="chartOptions" :series="series"></apexchart>
      </div>
    </div>
</template>
<script>
export default {
    name:"homeCharts",
      data: function () {
    return {
      //to add new chart change the code bootom and code in templte only
      //to add new chart change the code from here keep return and data function and code in templte only

      series: [{
            name: 'Total Income',
            data: []
          },],
          chartOptions: {
            title: {
              text: 'Total Income / Year',
              align: 'left'
            },
            chart: {
              height: 290,
              type: 'area'
            },
            dataLabels: {
              enabled: false
            },
            stroke: {
              curve: 'smooth'
            },
            xaxis: {
              type: 'datetime',
            categories: [""],

         //  categories: ["2018-01-19T00:00:00.000Z", "2018-09-19T01:30:00.000Z", "2018-09-19T02:30:00.000Z", "2018-09-19T03:30:00.000Z", "2018-09-19T04:30:00.000Z", "2018-09-19T05:30:00.000Z", "2018-09-19T06:30:00.000Z","2018-09-19T07:31:00.000Z", "2018-09-19T08:35:00.000Z", "2018-09-19T09:30:00.000Z", "2018-09-19T10:30:00.000Z", "2018-09-19T13:30:00.000Z", "2018-09-20T00:35:00.000Z", "2018-09-21T06:30:00.000Z","2018-09-22T00:00:00.000Z","2018-09-22T02:30:00.000Z","2018-09-22T04:30:00.000Z"]             
            },
            tooltip: {
              x: {
              format: 'dd/MM/yy HH:mm'
              },
            },
          },

      //end return
    };
  },
  mounted:function(){
      this.dailyChart();
  },
  methods:{
      dailyChart:function(){

          var x = 0 ;
          this.series[0].data = [null];
        var m = -1;
                for (let i = 0; i < 100; i++) {
        var billKey = "billKey" + i;

        if (localStorage.getItem(billKey) != null) {
          var retriveBillValue = JSON.parse(localStorage.getItem(billKey));
m = m+1;
      //    var outBillTotalProductsSold = retriveBillValue.billtotalproducts;
        


      //   sumOfTotalOutBillTotalProductsSold += Number(outBillTotalProductsSold);
          
         // console.log(sumOfTotalOutBillTotalProductsSold);
          //check DATE for line chart
          var outBillDate = retriveBillValue.billdatetime;
    //      console.log(outBillDate + "time and date form");
        var  splitoutBillDate = outBillDate.split("/");
//console.log("split result "+ splitoutBillDate);
        var dd = splitoutBillDate[0];
        var mm = splitoutBillDate[1];
        //split time and date
        var splitTimeAndDate = splitoutBillDate[2].split(" ");
        var yyyy= splitTimeAndDate[0];
        var date = yyyy+'-'+mm+'-'+dd ;
    //    console.log(date);
        //DATE'
        //to split time to hour and minute and secunds
        var splitTime = splitTimeAndDate[1];
 //       console.log(splitTime);
        var splitTimeToHMS = splitTime.split(":");
//time hh:mM:ss
        var hh= splitTimeToHMS[0];
        var mM= splitTimeToHMS[1];
        var ss= splitTimeToHMS[2];

//we should conver time and date tothis form 2018-09-19T01:30:00.000Z
  var newFormDateTime = date+"T"+hh+":"+mM+":"+ss+".000Z";
  console.log(newFormDateTime +"time date")
  this.chartOptions.xaxis.categories[m] = newFormDateTime;
 


     
     


 
        }
              
       
      
         
      } 
     
      
      this.chartOptions.xaxis.categories.sort();
      console.log(this.chartOptions.xaxis.categories);
      for (let n = 0 ;n < m+1 ;n++){
var getDateFromCharts = this.chartOptions.xaxis.categories[n];
//split for date
var splitGetDateFromCharts = getDateFromCharts.split("T");
var finalSplitGetDateFromCharts = splitGetDateFromCharts[0].split("-");
var chartsDate = finalSplitGetDateFromCharts[2]+"/"+finalSplitGetDateFromCharts[1]+"/"+finalSplitGetDateFromCharts[0];
//split fot time 
var splitGetTimeFromCharts = splitGetDateFromCharts[1].split(".");//00:00:00.0000Z
var chartsTime = splitGetTimeFromCharts[0];//00:00:00
var getTimeDateFromCharts = chartsDate +" "+chartsTime;
console.log(getTimeDateFromCharts);
        for (let i = 0; i < 100; i++) {
        billKey = "billKey" + i;

        if (localStorage.getItem(billKey) != null) {
          retriveBillValue = JSON.parse(localStorage.getItem(billKey));

      //    var outBillTotalProductsSold = retriveBillValue.billtotalproducts;
     var     outBillTotalBillPayment = retriveBillValue.billtotalpayment;


      //   sumOfTotalOutBillTotalProductsSold += Number(outBillTotalProductsSold);
          
         // console.log(sumOfTotalOutBillTotalProductsSold);
          //check DATE for line chart
          outBillDate = retriveBillValue.billdatetime;
          if( outBillDate == getTimeDateFromCharts){
            console.log(outBillDate);
            console.log("found date time equal ="+n )
       var splitoutBillTotalBill = outBillTotalBillPayment.split("$");
          
          x = Number(splitoutBillTotalBill[0]);
          console.log(x);
 this.series[0].data[n] = x;
          }
        }
        }

      }
     
      },
  },
}
</script>
<style lang="scss">
$darkBlueCol: #4736b1;
$greenCol: #56beb0;
$orangeCol:#FBA300;
$orangeOpCol:#fba300bb;
$whiteCol: #ffffff;
.home-chart{
    width: 100%;
    height: 300px;
    #chart{
        width: 50%;
        #area-chart{
  
          path{
            stroke: $darkBlueCol;
          
          }
          .apexcharts-toolbar{
            svg{
            stroke: $whiteCol;
          }}
        }
    }
}
</style>