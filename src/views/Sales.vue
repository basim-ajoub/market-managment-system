<template>
  <div class="sales-views">
    <h1>Sales</h1>

 <div id="line-chart-div">
        <apexchart class="line-chart" type="line" height="350" :options="chartOptions" :series="series"></apexchart>
      </div>
      <div id="pie-chart-div" class="pie-chart-div">
<ProductsSoldCharts class="pie-chart" />
      </div>


    
  </div>
</template>

<script>
import ProductsSoldCharts from "../components/sales/productsCharts.vue";
export default {
  
  name: "salesView",
  data: function () {
    return {
      //to add new chart change the code bootom and code in templte only
      //to add new chart change the code from here keep return and data function and code in templte only

   series: [{
              name: "Total Payments = $ ",
              data: []
          }],
          chartOptions: {
            chart: {
              height: 350,
              type: 'line',
              zoom: {
                enabled: false
              }
            },
            dataLabels: {
              enabled: false
            },
            stroke: {
              curve: 'straight'
            },
            title: {
              text: 'Total Income by Month 2021',
              align: 'left'
            },
            grid: {
              row: {
                colors: ['#4736b1', 'transparent'], // takes an array which will be repeated on columns
                opacity: 0.5
              },
            },
            xaxis: {
              categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep','Oct','Nov','Dec'],
            }
          },
          
          
      //end return

    };

    //end data
    
  },

  //end export\
  mounted: function () {
    this.changeValue();
  },
  components:{
    ProductsSoldCharts,
  },
  methods: {

    changeValue: function () {

    //   this.series[0].data[1] = 50;
      //    this.series = [8,200];
      //    this.series[0] = 40;
      //  this.chartOptions.labels[0] = "part1";

      //this.series[1] = 50;
      //this.chartOptions.labels[1] = "part2";

      //this.series[2] = 10;
      //this.chartOptions.labels[2] = "part3";
      //let n = 0;
      this.series[0].data = [0];
  var x = 0;
  var y = 0;
     var sumOfAllBillsTotalPayment = null ;
     //var sumOfTotalOutBillTotalProductsSold = null;
      for (let i = 100; i > 1; i--) {
        var billKey = "billKey" + i;

        if (localStorage.getItem(billKey) != null) {
          var retriveBillValue = JSON.parse(localStorage.getItem(billKey));

      //    var outBillTotalProductsSold = retriveBillValue.billtotalproducts;
          var outBillTotalBillPayment = retriveBillValue.billtotalpayment;


      //   sumOfTotalOutBillTotalProductsSold += Number(outBillTotalProductsSold);
          
         // console.log(sumOfTotalOutBillTotalProductsSold);
          //check DATE for line chart
          var outBillDate = retriveBillValue.billdatetime;
        var  splitoutBillDate = outBillDate.split("/");
        //DATE
        console.log(splitoutBillDate[0]+"-"+splitoutBillDate[1]);//1st one is day 2nd is month
 //loop to select the date by making tow lops one for months and other one for days
 for (let m=0 ; m<12;m++){//month loop
//check if bill month is the same with m
if(m == Number(splitoutBillDate[1]-1)){//we conver month to number for this reason  2 = 02  5 = 05


          var splitoutBillTotalBill = outBillTotalBillPayment.split("$");
          
          x = Number(splitoutBillTotalBill[0]);
      //  y = this.series[0].data[m] +x;
      if(this.series[0].data[m] == null){
        y = x ;
        this.series[0].data[m] == x ;
      }
else{
          console.log(this.series[0].data[m]+x ) ;
                   y = this.series[0].data[m]+x;
          console.log(y);
          
}
 this.series[0].data[m] =   y;
    

}

 }
 
        }
              
       
      
         
      } 
      if(sumOfAllBillsTotalPayment != null){
        console.log(sumOfAllBillsTotalPayment);
      //n  
      
     //  this.series[1] =String(sumOfTotalOutBillTotalProductsSold);
      //n   
     // this.chartOptions.labels[0] = "Total Payment";
     // this.chartOptions.labels[1] = "Total Sold Products";
      //  n=n+1;
      }
    },
  },
};
</script>

<style lang="scss">
$darkBlueCol: #4736b1;
$greenCol: #56beb0;
$orangeCol: #fba300;
$whiteCol: #ffffff;
.sales-views{
  width: 100%;
  height: 100%;
  h1{
    padding-top: 10px;
    margin-left: 1%;
    
  }
  #line-chart-div{
    margin-left: 3%;
    margin-top: 100px;
    width: 40%;
    height: 350px;
    float: left;

    .line-chart{
         width: 100%;
      path{
        stroke: $orangeCol;
      }


    }
  }
  #pie-chart-div{
width: 45%;
position: absolute;
right: 2%;
    margin-top: 100px;
    height: 350px;
    .pie-chart{

    }
  }
}
</style>
