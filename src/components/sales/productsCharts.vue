<template>
    <div class="products-charts">
<apexchart type="donut" :options="chartOptions" :series="series"></apexchart>
    </div>
</template>
<script>
export default {
    name:"productsChartsComp",
     data: function () {
    return {
      //to add new chart change the code bootom and code in templte only
      //to add new chart change the code from here keep return and data function and code in templte only
  
          
          series: [],
          chartOptions: {
                title: {
              text: 'Total Products',
              align: 'left'
            },
            chart: {
              type: 'donut',
            },
             labels: ["Total Sold Products .","Total Available Products ."],
            responsive: [{
              breakpoint: 480,
              options: {
                chart: {
                  width: 800
                },
                legend: {
                  position: 'bottom'
                }
              }
            }]
          
          }
          
          
        

      //end return
    };
     },

     methods:{
         countProductsforcharts:function(){
              var outBillProductsQuantity = null;
              var outStoreProductsQuantity = null;
              for (let i = 200; i > 1; i--) {
        var billKey = "billKey" + i;
        var productInfoKey = "productInfoKey"+i;

//to count total sold products
        if (localStorage.getItem(billKey) != null) {
            var retiriveBillInformation =JSON.parse(localStorage.getItem(billKey));
             outBillProductsQuantity += Number(retiriveBillInformation.billtotalproducts);
            this.series[0] = outBillProductsQuantity;
            console.log("check 1" +outBillProductsQuantity);
         }
         //to count number of products in market
         if(localStorage.getItem(productInfoKey) != null){
            var retiriveProductInformation =JSON.parse(localStorage.getItem(productInfoKey));
             outStoreProductsQuantity += Number(retiriveProductInformation.productquantity);
             this.series[1] = outStoreProductsQuantity;
             console.log("check 2" + outStoreProductsQuantity)
         }
              }
     },
     },
     mounted:function(){
         this.countProductsforcharts();//load pie charts function
     }
}
</script>
<style lang="scss">
$darkBlueCol: #4736b1;
$greenCol: #56beb0;
$orangeCol: #fba300;
$whiteCol: #ffffff;
.products-charts{

    width: 500px;
    height: 300px;
   

#SvgjsPath1170{
    fill: $darkBlueCol ;
}
#SvgjsPath1172{
    fill: $darkBlueCol ;
}
#SvgjsG1167{
    margin-top: 20px;
}

}
</style>