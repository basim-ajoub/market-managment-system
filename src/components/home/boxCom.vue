<template>
  <div class="box-comp">
   <h4 id="date-location">Date : <span v-bind="date" id="today-date">{{date}}</span> </h4> 
    <div class="box box1">
      <h3 id="paid-amount-1">0</h3>
      <a id="paid-icon-1"
        ><fontawesome-icon
          class="contact-icon"
          :icon="['fas', 'money-check-alt']"
      /></a>

      <h4 id="paid-title-1">Total Paid / Today</h4>
    </div>
    <div class="box box2">
      <h3 id="customers-amount-2">0</h3>
      <a id="customers-icon-2"
        ><fontawesome-icon class="icon" :icon="['fas', 'user-alt']"
      /></a>

      <h4 id="customers-title-2">Total Customers / Today</h4>
    </div>
    <div class="box box3">
      <h3 id="products-amount-3">0</h3>
      <a id="products-icon-3"
        ><fontawesome-icon class="icon" :icon="['fas', 'box-open']"
      /></a>

      <h4 id="products-title-3">Total Products / Today</h4>
    </div>
  </div>
</template>
<script>
export default {
  name: "boxComp",
  data:function(){
    return{
      date:"",
    }
  },
  mounted:function(){
    this.analysIncome();
  },
  methods:{
    analysIncome:function(){
  var totalProductForToday = 0;
  var totalCustomersForToday =0;
  var totalIncomeForToday = 0;
  var counter = 0;
  for (let i = 0; i < 100; i++) {
        var billKey = "billKey" + i;

        if (localStorage.getItem(billKey) != null) {
          var retriveBillValue = JSON.parse(localStorage.getItem(billKey));
          //retrieve bill date
          var billTimeDate = retriveBillValue.billdatetime;
          var splitbillTimeDate = billTimeDate.split(" ");
          var billDate = splitbillTimeDate[0];
          // today date 
            var today = new Date();
      var dd = String(today.getDate()).padStart(2, "0");
      var mm = String(today.getMonth() + 1).padStart(2, "0");
      var yyyy = today.getFullYear();
      today = dd + "/" + mm + "/" + yyyy;
this.date = today ;
if(billDate == today){
 counter = counter + 1; 
  console.log(retriveBillValue.billtotalpayment + "date= today" + billDate);
  totalProductForToday = Number(totalProductForToday) + Number(retriveBillValue.billtotalproducts);
  totalCustomersForToday = counter;
  var splitIncomeForToday = retriveBillValue.billtotalpayment.split("$");
  totalIncomeForToday = totalIncomeForToday + Number(splitIncomeForToday[0]);
document.getElementById("paid-amount-1").innerText ="$ " + totalIncomeForToday ;
document.getElementById("products-amount-3").innerText = totalProductForToday;
document.getElementById("customers-amount-2").innerText = totalCustomersForToday;
  

}
        }
                    }

    },
  },
};
</script>
<style lang="scss">
$darkBlueCol: #4736b1;
$greenCol: #56beb0;
$orangeCol:#FBA300;
$orangeOpCol:#fba300bb;
$whiteCol: #ffffff;
.box-comp {
  width: 100%;
  height: 220px;
#date-location{
  position: absolute;
  right: 4%;
  top: 20px;
  color: $darkBlueCol;
}
  .box {
    width: 28%;
    height: 150px;
background: rgb(58,51,171);
background: linear-gradient(42deg, $darkBlueCol 0%, $darkBlueCol 52%, $greenCol 100%);
//background: rgb(58,51,171);
//background: linear-gradient(70deg, rgba(58,51,171,1) 0%, rgba(71,54,177,1) 78%, rgba(251,163,0,1) 100%);
    float: left;
    margin-left: 4%;
    border: 1px solid $greenCol;
    border-radius: 7%;
    position: relative;
    cursor: pointer;
    color: $whiteCol;
    transition: 0.4s ease-in-out;
    overflow: hidden;
    &:hover{
        width: 30%;
        height: 157px;
        background: linear-gradient(42deg, $darkBlueCol 0%, $darkBlueCol 52%, $orangeCol 100%);
    }
    h3{
        font-weight: bolder;
        font-size: 30px;
        margin-left: 6%;
        margin-top: 10px;
    }
  
    a{
        position: absolute;
        top: 45px;
        right: 4%;
        font-size: 60px;
    }
    h4{
        margin-left: 6%;
        margin-top: 62px;
        font-weight: bold;
    }
  }
}
</style>
