<template>
  <div class="add-new-product">
    <h1>Add New Products Form</h1>
    <form class="add-product-form" action="submit">
      <p>Name :</p>
      <input id="product-name" type="text" /><br />
      <p>Type:</p>
      <select name="add-products-type" id="add-products-type">
        <option value="drinks">Drinks</option>
        <option value="foods">Foods</option>
        <option value="cigarettes">Cigarettess</option></select
      ><br />
      <p >Price :</p>
      <input id="product-price" type="number" /><br />
      <p >Code :</p>
      <input id="product-code" type="text" /><br />
      <p>Quantity :</p>
      <input id="product-quantity" type="number" /><br />
      <p>Size :</p>
      <input type="text" id="product-size"><br>
       <p>Status : </p>
       <select name="check-availability-product" id="availabilty-product">
         <option value="available">Available</option>
         <option value="not-available">Not Available</option>

         </select><br />
    </form>
    <button @click="saveNewProduct" class="add-product-btn">
     Save
    </button>
  </div>
</template>
<script>
export default {
  name: "addProductView",

  methods: {

    saveNewProduct: function () {
      const inpProductName = document.getElementById("product-name").value;
      const inpProductType = document.getElementById("add-products-type").value;
      const inpProductPrice = document.getElementById("product-price").value;
      const inpProductSize = document.getElementById("product-size").value;
      const inpProductQuantity =
        document.getElementById("product-quantity").value;
      const inpProductCode = document.getElementById("product-code").value;
      var inpProductavailabilty = document.getElementById("availabilty-product").value;
      var inpProductStatus = ""; 
      if(inpProductQuantity > 0 && inpProductavailabilty == "available"){
        inpProductStatus = "Available";
        
      }
      else{
        inpProductStatus = "Not Available";
      }
      console.log( inpProductName + inpProductType + inpProductPrice + inpProductQuantity + inpProductCode);
      var productInfoValue = {
        productname: inpProductName,
        productprice: inpProductPrice,
        producttype : inpProductType,
        productquantity: inpProductQuantity,
        productcode: inpProductCode,
        productsize:inpProductSize,
        productstatus: inpProductStatus,
      };
      if (
        inpProductName &&
        inpProductPrice &&
        inpProductType &&
        inpProductQuantity &&
        inpProductSize &&
        inpProductCode !== ""
      ) {
      let i = localStorage.length + 1;
          const productInfoKey = "productInfoKey" + i;
          //conver it to string becouse localstorage accept only string fot lists
          var productInfoValueSerialized = JSON.stringify(productInfoValue);
          //end converting
          localStorage.setItem(productInfoKey, productInfoValueSerialized);
        location.reload();
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
.add-new-product {
  width: 100%;
  height: 620px;
  h1{
    margin-left: 1%;
    margin-top: 10px;
  }
  .add-product-form {
    width: 60%;
    margin-top: 100px;
    margin-left: 2%;

    p {
      float: left;
      margin-top: 20px;
      width: 17%;
      font-weight: bold;
    }
    #add-products-type,
    input,#availabilty-product {
      width: 40%;
      height: 25px;
      margin-top: 15px;
      border-radius: 5%;
    }
  }
  .add-product-btn {
    width: 7%;
    height: 25px;
    margin-top: 160px;
    
    margin-left: 85%;
    position: relative;
    cursor: pointer;
    z-index: 1;
   
  
      
    
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
      transition: 0.4s all ease;
      float: left;
    a {
      width: 100%;
      display: block;
 
      
    }
    &::before {
        width: 99%;
        height: 0%;
        background: $orangeCol;
        content: "";
        position: absolute;
        top: 50%;
        border-radius: 10%;
        right: 50%;
        z-index: -1;
        transform: translate(50%, -50%);
        transition: 1ms all ease;
        border-top-left-radius: 40%;
           border-bottom-left-radius: 40%;
    }
     &:hover::before {
        width: 100%;
        height: 100%;
      }
    &:hover{
            
         box-shadow: 0px 0px 3px 3px $orangeCol;
        border: 1.5px solid $orangeCol;
        border-radius: 10%;
        transition: 0.6s ease;
        color: $whiteCol;
        font-weight: bolder;
          }
  }
}
</style>
