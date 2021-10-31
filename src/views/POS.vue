<template>
  <div class="pos-views">
    <h1>POS</h1>
    <div class="btn-list">
      <button class="pos-btn">
        <router-link to="/addnewpos">Add New POS</router-link>
      </button>
      <button @click="enterPosNumberField" class="pos-btn" id="edit-pos-btn">
       Edit Old POS
      </button>
      <input type="text" name="" id="pos-edit-field" placeholder="Type POS Number">
      <button @click="viewBillCard" id="show-pos" class="show-pos">+</button>
    </div>
    <div class="poss-table">
      <table id="show-all-pos-table" class="show-all-pos-table">
        <tr class="main-row">
          <th class="width1">No.</th>
          <th class="width2">Bill No.</th>
          <th class="width2">Date</th>
          <th class="width3">Employer's Name</th>
          <th class="width1">Total Products</th>
          <th class="width1">Total Bill</th>
          <th class="width1">Tax</th>
          <th class="width1">Discount</th>
          <th class="width1">Total Payment</th>
        </tr>
      </table>
    </div>
    <div id="show-edit-pos" class="show-edit-pos">
      <button @click="closeWindow" class="close-btn" id="close-btn">X</button>
      <div id="pos-card" class="pos-card">
        <h2>Edit Existing Bill</h2>
<section class="bill-no">
        <p>Bill No. :</p>
        <span id="bill-number"></span>
        <input id="edit-bill-number"><br /><br>
      </section>
      <section>
        <p>Products :</p>
        <input type="number" id="edit-total-products">
      </section>
      <br />
      <section>
        <p>Total :</p>
        <input type="text" id="edit-total-bill-without-tax">
      </section>
      <br />
      <section>
        <p>Discount :</p>
        <input type="text" placeholder="Discount Code" id="edit-discount" />
      </section>
      <br />
      <section>
        <p>Tax :</p>
        <input id="edit-tax-value">
      </section>
      <br />
      <section>
        <p>Total Bill:</p>
        <span id="edit-bill-with-tax-discount"> 0$ </span>
      </section>
      <button @click="updateBill" id="update-btn">Update</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "allPos",
  mounted: function () {
    this.showAllBills();
  },
  methods: {
    showAllBills: function () {
      var n = 0;
      for (let i = 100; i > 1; i--) {
        var billKey = "billKey" + i;

        if (localStorage.getItem(billKey) != null) {
          n = n + 1;
          var retriveBillValue = JSON.parse(localStorage.getItem(billKey));
          var outBillNumber = retriveBillValue.billnumber;
          var outBillDateTime = retriveBillValue.billdatetime;
          var outBillTotalBill = retriveBillValue.billtotalbill;
          var outBillTax = retriveBillValue.billtax;
          var outBillDiscount = retriveBillValue.billdiscount;
          var outBillTotalPayment = retriveBillValue.billtotalpayment;
          var outBillTotalProducts = retriveBillValue.billtotalproducts;
          document.getElementById("show-all-pos-table").innerHTML +=
            '<tr class="normal-row"><td class="width1">' +
            n +
            '</td><td class="width2">' +
            outBillNumber +
            '</td><td class="width3">' +
            outBillDateTime +
            '</td><td class="width3">Juhans Mohan</td><td class="width1">' +
            outBillTotalProducts +
            '</td><td class="width1">' +
            outBillTotalBill +
            '</td><td class="width1">' +
            outBillTax +
            '</td><td class="width1">' +
            outBillDiscount +
            '</td><td class="width1">' +
            outBillTotalPayment +
            "</td></tr>";
          console.log(retriveBillValue);
        }
      }
     
    },
     enterPosNumberField:function(){
       document.getElementById("show-pos").style.display = "block";
       document.getElementById("pos-edit-field").style.display = "block";
      },
//Start View Bill
viewBillCard:function(){
     var inpEditBillNo = document.getElementById("pos-edit-field").value;
      document.getElementById("show-edit-pos").style.display = "block";

        
     for(let i=1 ; i<localStorage.length+100 ;i++){
      //bill information
     var billKey = "billKey" + i;
      if (localStorage.getItem(billKey) != null) {
        var retriveBillValue = JSON.parse(localStorage.getItem(billKey));
        if(retriveBillValue.billnumber == inpEditBillNo){
        document.getElementById("bill-number").innerText = inpEditBillNo;
        var oldEditBillNo =  document.getElementById("bill-number").innerText;
        document.getElementById("edit-bill-number").value = oldEditBillNo;


       document.getElementById("edit-total-bill-without-tax").value = retriveBillValue.billtotalbill;
        document.getElementById("edit-total-products").value = retriveBillValue.billtotalproducts;
   document.getElementById("edit-discount").value = retriveBillValue.billdiscount
     document.getElementById("edit-tax-value").value= retriveBillValue.billtax;
        }
        }
     }
},
      //Start Update bill
        updateBill: function () {
          var inpEditBillNo = document.getElementById("pos-edit-field").value;

        
     for(let i=1 ; i<localStorage.length+100 ;i++){
      //bill information
     var billKey = "billKey" + i;
      if (localStorage.getItem(billKey) != null) {
        var retriveBillValue = JSON.parse(localStorage.getItem(billKey));
        if(retriveBillValue.billnumber == inpEditBillNo){
 
    var newTotalBillWithoutTax =  document.getElementById("edit-total-bill-without-tax").value;
    var newDiscountValue =      document.getElementById("edit-discount").value;
    var newTaxValue = document.getElementById("edit-tax-value").value;
var newBillNumber = document.getElementById("edit-bill-number").value ;
var newProductsNumber = document.getElementById("edit-total-products").value ;
 var splitnewDiscountValue = newDiscountValue.split("$");
 var splitnewTaxValue = newTaxValue.split("$");
 var splitnewTotalBillWithoutTax = newTotalBillWithoutTax.split("$");
console.log(splitnewTotalBillWithoutTax[0] +splitnewTaxValue[0] + splitnewDiscountValue[0] )
      var newBilltotalpayment = Number(splitnewTotalBillWithoutTax[0]) + Number(splitnewTaxValue[0]) - Number(splitnewDiscountValue[0]) ;
    var savenewBilltotalpayment =    document.getElementById("edit-bill-with-tax-discount").innerText= newBilltotalpayment +"$";
    

        var billValue = {
          billnumber: newBillNumber,
          billdatetime:retriveBillValue.billdatetime,
          billtotalbill: newTotalBillWithoutTax,
          billdiscount: newDiscountValue,
          billtax: newTaxValue,
          billtotalpayment: savenewBilltotalpayment,
          billtotalproducts: newProductsNumber,
        };
        var serializedbillValue = JSON.stringify(billValue);
        localStorage.setItem(billKey, serializedbillValue);
      }

     }
     }
     location.reload();
    },
    closeWindow:function(){
      document.getElementById("show-edit-pos").style.display="none";
    },
  },
};
</script>

<style lang="scss">
$darkBlueCol: #4736b1;
$greenCol: #56beb0;
$orangeCol: #fba300;
$whiteCol: #ffffff;
.pos-views {
  background: $whiteCol;
  width: 100%;
  height: 97%;
  padding-top: 10px;

  h1 {
    margin-left: 1%;
  }
  .btn-list {
    width: 40%;
    height: 35px;
    margin-left: 1%;
    margin-top: 40px;
#pos-edit-field{
  width: 35%;

  display: none;
  float: left;
}
#show-pos{
  margin-top: 10px;
  width: 5%;
  cursor: pointer;
  display: none;
}

    .pos-btn {
      width: 25%;
      height: 28px;
      margin-right: 3%;
      background: $whiteCol;
      border-radius: 12%;
      border: 1.5px solid $darkBlueCol;
      transition: 0.6s all ease;
      position: relative;
      box-shadow: 1px 1px 1px 2px $darkBlueCol;
      z-index: 1;
      overflow: hidden;
     color: $darkBlueCol;
      cursor: pointer;
      transition: 1s all ease;
      float: left;
      a{
        color: $darkBlueCol;
      }
      &::before {
        width: 100%;
        height: 0%;
        background: $orangeCol;
        content: "";
        position: absolute;
        top: 50%;
        border-radius: 10%;
        right: 50%;
        z-index: -1;
        transform: translate(50%, -50%);
        transition: 0.4s all ease;
        border-top-left-radius: 40%;
      border-bottom-left-radius: 40%;

      }
      &:hover::before {
        width: 100%;
        height: 100%;
      }
  
      &:hover {
        box-shadow: 0px 0px 3px 3px $orangeCol;
        border: 1.5px solid $orangeCol;
        border-radius: 10%;
        transition: 0.6s ease;
        color: $whiteCol;
        font-weight: bolder;
        a {
          color: $whiteCol;
          font-weight: bold;
        }
      }
    }
  }
  .poss-table {
    width: 98%;
    height: 490px;
    background: $whiteCol;
    margin-left: 1%; 
     overflow: hidden;
    overflow-y: scroll;
  
    border: 2px solid $greenCol;
    .show-all-pos-table {
      width: 100%;
      text-align: center;
      .normal-row{
cursor: pointer;
height: 60px;
border: 1px solid black;
} 
 .normal-row:hover{

    background: $orangeCol;
  }
      .main-row {
        height: 50px;

        background: $greenCol;

      }
      .width1 {
        width: 2%;
      }
      .width2 {
        width: 7%;
      }
      .width3 {
        width: 10%;
      }
    }
  }
  .show-edit-pos{
    width: 100%;
    background: rgba(0, 0, 0, 0.719);
display: none;
    height: 100%;
    position: absolute;
    top: 0;
    z-index: 8;
    left: 0;
    #close-btn{
      cursor: pointer;
      width: 2.5%;
      height: 22.5px;
      position: absolute;
      right: 2%;
      top: 10px;
      font-size: 17px;
      font-weight: bolder;
    }
    .pos-card{
      width: 30%;
      height: 400px;
      background: $whiteCol;
      margin-left: 35%;
      margin-top: 100px;
      z-index: 9;
      opacity: 1;
      border-radius: 12%;
      border: 1px solid $darkBlueCol;
      
      h2{
        color: $orangeCol;
        margin-top: 10px;
        text-align: center;
      margin-bottom: 20px;
      margin-left: 2%;
      }
      .bill-no{
        #bill-number{
          display: none;
        }
        #edit-bill-number{

        }
      }
      section{
        margin-bottom: 15px;
      }
        p {
      width: 35%;
      font-size: 15px;
      font-weight: bold;
      float: left;
      margin-left: 2%;
    }
    span {
      font-weight: bolder;
      font-size: 16px;
    }
    #edit-tax-value {
      overflow: hidden;
    }
    #edit-bill-with-tax-discount {
      font-size: 20px;
    }
    input {
      width: 50%;
      height: 15px;
      border: 1px solid $darkBlueCol;
      border-radius: 2%;
      &::placeholder {
        color: $orangeCol;
      }
    }
    #update-btn {
      width: 25%;
      height: 25px;
      margin-top: 5px;
      margin-left: 65%;
      cursor: pointer;
      transition: 0.1s ease-in-out;
      border-radius: 10%;
      &:hover{
        width: 26%;
        height: 26px;
        background: $orangeCol;
        font-weight: bold;
        color: $whiteCol;
      }
    }
      
    }
  }
}
</style>
