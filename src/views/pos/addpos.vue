<template>
  <div class="add-new-pos">
    <h1>New Customer :</h1>
    <div class="add-product-form">
      <input
        id="product-code-toadd"
        type="text"
        placeholder="Enter Product's Code"
      />
      <button @click="AddProductToPOS" class="add-btn">Add</button>
      <span id="status-not-available">Not Availble</span>
    </div>
    <div class="pos-div">
      <form action="submit" class="pos-form">
        <table id="pos-table">
          <tr class="main-row">
            <th class="width1">No.</th>
            <th class="width3">Product</th>
            <th class="width2">Code</th>
            <th class="width1">Prise</th>
            <th class="width1">Quantity</th>
            <th class="width1">Total Price</th>
          </tr>
        </table>
      </form>
    </div>
    <!--Start Total Bill -->
    <div class="total-bill-div">
      <section class="bill-no">
        <p>Bill No. :</p>
        <span id="bill-number"></span><br />
        <p>Date :</p>
        <span id="date-now"></span><br />
        <p>Time :</p>
        <span id="time-now"></span>
      </section>
      <section>
        <p>Products :</p>
        <span id="total-products">0</span>
      </section>
      <br />
      <section>
        <p>Total :</p>
        <span id="total-bill-without-tax">0$ </span>
      </section>
      <br />
      <section>
        <p>Discount :</p>
        <input type="text" placeholder="Discount Code" />
        <span id="discount-value"> 0$</span>
      </section>
      <br />
      <section>
        <p>Tax :</p>
        <span id="tax-value">0$ </span>
      </section>
      <br />
      <section>
        <p>Total Bill:</p>
        <span id="bill-with-tax-discount"> 0$ </span>
      </section>
      <br />
      <button ref="/pos" @click="printBill" class="print-btn">
       Print
        
      </button>
    </div>
    <!--End Total Bill -->
  </div>
</template>

<script>
export default {
  name: "addPos",
  data() {
    return {
      n: 0,
    };
  },
  mounted: function () {
    this.generateBillNumber(); //run function to generate random bill number
  },
  methods: {
    AddProductToPOS: function () {
      //Start get date

      var today = new Date();
      // or    var GermanTime = today.toLocaleTimeString();
      var dd = String(today.getDate()).padStart(2, "0");
      var mm = String(today.getMonth() + 1).padStart(2, "0");
      var yyyy = today.getFullYear();
      var GermanTime = today.toTimeString();
      var splitGermanTime = GermanTime.split(" "); //to get only time in 24hour
      //for time in 12 hour
      //var GermanTime = today.toLocaleTimeString();

      today = dd + "/" + mm + "/" + yyyy;
      console.log(splitGermanTime[0]); //edit to change
      document.getElementById("date-now").innerText = today;
      document.getElementById("time-now").innerText = splitGermanTime[0];
      //End Set date

      const InpProductCode =
        document.getElementById("product-code-toadd").value;
      let InpTotalBillWT = document.getElementById(
        "total-bill-without-tax"
      ).innerText;

      let n = this.n + 1;

      //Start Loop To Get All Products in LocalStorage
      for (let j = 1; j < localStorage.length + 1; j++) {
        var productInfoKey = "productInfoKey" + j;
        //Start Ignor Null Values and Get Products by products Key from localstorage
        if (localStorage.getItem(productInfoKey) !== null) {
          let productInfoValueRetieve = JSON.parse(
            localStorage.getItem(productInfoKey)
          );

          //Check Product Code To Add
          if (productInfoValueRetieve.productcode == InpProductCode) {
            //Check product if it is already register

            var checkCoddeIfExist = document.getElementById(
              "product-code-element-" + j
            );

            //to reduce the quantity number
            var newproductquantity =
              Number(productInfoValueRetieve.productquantity) - 1;
            //Check Quantity to Change Availability
            var newProductAvailabilty = "";
            if (newproductquantity > 0) {
                   document.getElementById("status-not-available").style.display="none";
              newProductAvailabilty = "Available";
              if (
                typeof checkCoddeIfExist != "undefined" &&
                checkCoddeIfExist != null
              ) {
                if (checkCoddeIfExist.innerText == InpProductCode) {
                  console.log("you have already registered the product");
                  document.getElementById(
                    "product-quantity-buying-" + j
                  ).value =
                    Number(
                      document.getElementById("product-quantity-buying-" + j)
                        .value
                    ) + 1;
                }
              } else {
                document.getElementById("pos-table").innerHTML +=
                  '<tr class="normal-row"><td class="width1">' +
                  n +
                  '</td><td class="width3">' +
                  productInfoValueRetieve.productname +
                  '</td><td class="width2" id="product-code-element-' +
                  j +
                  '">' +
                  productInfoValueRetieve.productcode +
                  '</td><td class="width1">' +
                  productInfoValueRetieve.productprice +
                  " $" +
                  '</td><td class="width1"><input class="quantity-product" id="product-quantity-buying-' +
                  j +
                  '" value="1" type="number" /></td><td id="total-price-to-multiply-' +
                  j +
                  '" class="width1" >' +
                  productInfoValueRetieve.productprice +
                  " $" +
                  "</td></tr>";
              }

              var newProductInfoValue = {
                productname: productInfoValueRetieve.productname,
                productcode: productInfoValueRetieve.productcode,
                productprice: productInfoValueRetieve.productprice,
                productsize: productInfoValueRetieve.productsize,
                producttype: productInfoValueRetieve.producttype,
                productquantity: newproductquantity,
                productstatus: newProductAvailabilty,
              };
              var newProductInfoValueSerialized =
                JSON.stringify(newProductInfoValue);
              localStorage.setItem(
                productInfoKey,
                newProductInfoValueSerialized
              );

              // to make total and prise math calculation for products

              //multiplt quantit with prise
              var totalSameProductsquantity = Number(
                document.getElementById("product-quantity-buying-" + j).value
              );
              var productPrise = productInfoValueRetieve.productprice;
              document.getElementById(
                "total-price-to-multiply-" + j
              ).innerText = productPrise * totalSameProductsquantity + " $";

              InpTotalBillWT = document.getElementById(
                "total-price-to-multiply-" + j
              ).innerText;
              //It Is string we should take the prise without $ sign by split()
              var splitInpTotalBillWT = InpTotalBillWT.split("$");
              //it  is string value we should convert it to numrical value by using Number()
              var convToNumsplitInpTotalBillWT = Number(splitInpTotalBillWT[0]);
              console.log(convToNumsplitInpTotalBillWT);
              // add it to total bill without tax
              //to calculate discount and add it

              var checkDiscount =
                document.getElementById("discount-value").innerText;
              var splitcheckDiscount = checkDiscount.split("$");
              var numirecalCheckDiscount = splitcheckDiscount[0];

              //we take the contains total bill to add the prise for the new product
              var OutputTotalBillWT = document.getElementById(
                "total-bill-without-tax"
              ).innerText;
              var splitOutputTotalBillWT = OutputTotalBillWT.split("$");
              var convToNumsplitOutputTotalBillWT = Number(
                splitOutputTotalBillWT[0]
              );
              var addPriseToToatalbill =
                convToNumsplitOutputTotalBillWT +
                Number(productInfoValueRetieve.productprice);
              document.getElementById("total-bill-without-tax").innerText =
                addPriseToToatalbill + " $";

              // check and calculate tax
              document.getElementById("tax-value").innerText =
                document.getElementById("total-bill-without-tax").innerText;
              var checkTax = document.getElementById("tax-value").innerText;
              var splitcheckTax = checkTax.split("$");
              var numirecalCheckTax = splitcheckTax[0];
              //5% tax to the bill
              document.getElementById("tax-value").innerText =
                numirecalCheckTax * 0.05 + " $";
              // to take only tax value
              var taxValue = document.getElementById("tax-value").innerText;
              var splitTaxValue = taxValue.split("$");
              var numercalTaxValue = splitTaxValue[0];
              //calculate all bill with tax and discount

              // total bill = tax 5% + discount + total bill

              var total =
                Number(numercalTaxValue) +
                Number(addPriseToToatalbill) -
                Number(numirecalCheckDiscount);
              document.getElementById("bill-with-tax-discount").innerText =
                total + " $";

              //count the products
              var totalProductsBuying = Number(
                document.getElementById("total-products").innerText
              );
              totalProductsBuying = totalProductsBuying + 1;
              document.getElementById("total-products").innerText =
                totalProductsBuying;
            } else {
              newProductAvailabilty = "Not Available";
              document.getElementById("status-not-available").style.display="block";
              document.getElementById("status-not-available").innerText =
                "The Product Is Not Available";
            }
          }
         
        }
      }
    },
    generateBillNumber: function () {
      var randomNumber = Math.random() * 100000000000000000;
      document.getElementById("bill-number").innerText = randomNumber;
    },
    printBill: function () {
      var j = localStorage.length + 2;
      var billKey = "billKey" + j;
      //bill information
      if (localStorage.getItem(billKey) == null) {
        var inpbillnumber = document.getElementById("bill-number").innerText;
        var inpbilldate = document.getElementById("date-now").innerText;
        var inpbilltime = document.getElementById("time-now").innerText;
        var inpbilltotalbill = document.getElementById(
          "total-bill-without-tax"
        ).innerText;
        var inpbilldiscount =
          document.getElementById("discount-value").innerText;
        var inpbilltax = document.getElementById("tax-value").innerText;
        var inpbilltotalpayment = document.getElementById(
          "bill-with-tax-discount"
        ).innerText;
        var inpbillproducts =
          document.getElementById("total-products").innerText;
        var billValue = {
          billnumber: inpbillnumber,
          billdatetime: inpbilldate + " " + inpbilltime,
          billtotalbill: inpbilltotalbill,
          billdiscount: inpbilldiscount,
          billtax: inpbilltax,
          billtotalpayment: inpbilltotalpayment,
          billtotalproducts: inpbillproducts,
        };
        var serializedbillValue = JSON.stringify(billValue);
        localStorage.setItem(billKey, serializedbillValue);
      } else {
        j = localStorage.length + 5;
        billKey = "billKey" + j;
        inpbillnumber = document.getElementById("bill-number").innerText;
        inpbilldate = document.getElementById("date-now").innerText;
        inpbilltime = document.getElementById("time-now").innerText;
        inpbilltotalbill = document.getElementById(
          "total-bill-without-tax"
        ).innerText;
        inpbilldiscount = document.getElementById("discount-value").innerText;
        inpbilltax = document.getElementById("tax-value").innerText;
        inpbilltotalpayment = document.getElementById(
          "bill-with-tax-discount"
        ).innerText;
        inpbillproducts = document.getElementById("total-products").innerText;
        billValue = {
          billnumber: inpbillnumber,
          billdatetime: inpbilldate + " " + inpbilltime,
          billtotalbill: inpbilltotalbill,
          billdiscount: inpbilldiscount,
          billtax: inpbilltax,
          billtotalpayment: inpbilltotalpayment,
          billtotalproducts: inpbillproducts,
        };
        serializedbillValue = JSON.stringify(billValue);
        localStorage.setItem(billKey, serializedbillValue);
      }

      location.reload();
    },
  },
  watch: {},
};
</script>
<style lang="scss">
$darkBlueCol: #4736b1;
$greenCol: #56beb0;
$orangeCol: #fba300;
$whiteCol: #ffffff;
.add-new-pos {
  width: 100%;
  height: 100%;
  background: $whiteCol;

  h1 {
    margin-bottom: 50px;
    margin-left: 1%;
    padding-top: 10px;
  }
  .add-product-form {
    margin-left: 1%;
    width: 95%;
    height: 30px;
    input {
      width: 19%;
      height: 23px;
      margin-right: 1%;
      border: 1.5px solid $darkBlueCol;
      border-radius: 2%;
      box-shadow: 0px 0px 1px 1px $darkBlueCol;
      float: left;
      &::placeholder {
        color: $darkBlueCol;
      }
    }
    #status-not-available {
      width: 20%;
      display: none;
      margin-left: 1.5%;
      font-size: 14px;
      font-weight: bold;
      float: left;
    }
    .add-btn {
      width: 6%;
      height: 26px;
      cursor: pointer;
      background: $whiteCol;
      border: 1.5px solid $darkBlueCol;
      box-shadow: 1px 1px 1px 2px $darkBlueCol;
      border-radius: 10%;
      position: relative;
      transition: 1s all ease;
      float: left;
      color:$darkBlueCol;
      z-index: 1;
      &::before {
        width: 100%;
        height: 0%;
        background: $orangeCol;
        border-top-left-radius: 40%;
        border-bottom-left-radius: 40%;
        content: "";
        position: absolute;
        top: 50%;
        right: 50%;
        z-index: -1;
        transform: translate(50%, -50%);
        transition: 0.6s all ease;
      }
      &:hover::before {
        width: 100%;
        height: 100%;
      }
      &:hover {
        box-shadow: 0px 0px 1px 1px $orangeCol;
        border: 1.5px solid $orangeCol;
        border-radius: 10%;
        transition: 0.6s ease;

        color: $whiteCol;
        font-weight: bold;
      }
    }
  }
  .pos-div {
    margin-left: 1%;
    width: 74%;
    background: $whiteCol;
    float: left;

    .pos-form {
      width: 100%;
      height: 500px;
      overflow: hidden;
      overflow-y: scroll;
      #pos-table {
        width: 100%;
        text-align: center;

        .main-row {
          height: 40px;
          background: $greenCol;
        }

        .width1 {
          width: 4%;
          .quantity-product {
            width: 50%;
          }
        }
        .width2 {
          width: 7%;
        }
        .width3 {
          width: 20%;
        }
      }
    }
  }
  .total-bill-div {
    width: 23%;
    height: 350px;
    background: $greenCol;
    box-shadow: 0px 0.5px 5px 5px $darkBlueCol;
    margin-left: auto;
    margin-right: 1%;
    padding-top: 20px;
    .bill-no {
      margin-bottom: 40px;
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
    #tax-value {
      overflow: hidden;
    }
    #bill-with-tax-discount {
      font-size: 20px;
    }
    input {
      width: 35%;
      height: 15px;
      border: 1px solid $darkBlueCol;
      border-radius: 2%;
      &::placeholder {
        color: $darkBlueCol;
      }
    }
    .print-btn {
      width: 25%;
      height: 25px;
      margin-top: 20px;
      margin-left: 70%;
      cursor: pointer;
      #print-link {
        width: 100%;
        height: 14px;
      }
    }
  }
}
</style>
