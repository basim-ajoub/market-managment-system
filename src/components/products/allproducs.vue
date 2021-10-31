<template>
  <div id="allproducts" class="allproducts">
    <div v-bind="showAllProductss()" id="test-all-products-tp-show">
      <SingleProduct
        v-for="x in series"
        :key="x.key"
        :productname="x.productname"
        :productsize="x.productsize"
        :productprise="x.productprice"
        :producttype="x.producttype"
        :productcode="x.productcode"
        :productquantity="x.productquantity"
      />
    </div>
    <div id="view-product-to-edit" class="view-product-to-edit">
      <button @click="closeEditProductWindow" id="close-btn">X</button>
      <div class="products-box">
    <div class="box-img">
      <img src="logo.png" alt="" />
    </div>
    <div class="box-discription">
      <p id="hidden-code-to-compare">hidden</p><!--hidden to get the product from local storage-->
        <p>Name : <input type="text" id="edit-name-field" ></p>
        <p>Type : <select name="add-products-type" id="edit-add-products-type">
        <option value="drinks">Drinks</option>
        <option value="foods">Foods</option>
        <option value="segarets">Segarets</option></select
      ></p> 
        <p>Price : <input type="number" id="edit-price-field"> </p>
        <p >Quantity : <input type="number" id="edit-quantity-field"></p>
        <p>Size : <input type="text" id="edit-size-field"></p>
          <p>Code : <input type="text" id="edit-code-field"></p>
    </div>
          <div class="btn-list">
            <button class="color"  @click="updateExistProduct" id="update-btn">Update</button>
            <button class="color" id="delete-btn">Delete</button>
          </div>
  </div>
    </div>
  </div>
</template>
<script>
import SingleProduct from "../products/prodct.vue";
export default {
  name: "allProductsComp",
  data: function () {
    return {
      //localsto : {'key':[1,2,5,7,8,9,10],
      //           'keyy':[1,2,5,7,8,9,10],
      //},
      series: [
        {
        }
      ],
    };
  },

  components: {
    SingleProduct,
  },
  props: { SingleProduct },
  mounted: function () {
    this.showAllProductss();
  },
  methods: {

    showAllProductss: function () {
      var n = 0;
      for (let i = 1; i < 200; i++) {
        var productInfoKey = "productInfoKey" + i;
        if (localStorage.getItem(productInfoKey) != null) {
          var retriveProductValue = JSON.parse(localStorage.getItem(productInfoKey));
this.series[n] = retriveProductValue;
         // this.series[n].productname = retriveProductValue.productname;
          console.log( this.series[n]);
  n = n + 1;
          
        }
      
      }
      
    },
  closeEditProductWindow:function(){
document.getElementById("view-product-to-edit").style.display = "none";
  },
    updateExistProduct:function(){
      var getSelectedProductCode = document.getElementById("hidden-code-to-compare").innerText;
         var     Editedproductname= document.getElementById("edit-name-field").value;
        var     Editedproductprice= document.getElementById("edit-price-field").value;
        var     Editedproducttype = document.getElementById("edit-add-products-type").value;
        var     Editedproductquantity= document.getElementById("edit-quantity-field").value;
        var     Editedproductcode= document.getElementById("edit-code-field").value;
        var     Editedproductsize= document.getElementById("edit-size-field").value;
      for(let i=1 ; i<localStorage.length+100;i++){
         var productInfoKey = "productInfoKey" + i;
if(localStorage.getItem(productInfoKey) != null){
       var retriveProductValue = JSON.parse(localStorage.getItem(productInfoKey));
if( retriveProductValue.productcode == getSelectedProductCode){
  var productInfoValue = {
        productname: Editedproductname,
        productprice: Editedproductprice,
        producttype :Editedproducttype,
        productquantity:Editedproductquantity,
        productcode: Editedproductcode,
        productsize:Editedproductsize,
      };
    var productInfoValueSerialized = JSON.stringify(productInfoValue);
     localStorage.setItem(productInfoKey, productInfoValueSerialized);
        location.reload();
}
}

      }
    },

  },
};
</script>
<style lang="scss">
$darkBlueCol:#4736B1;
$greenCol:#56BEB0;
$orangeCol:#FBA300;
$orangeOpCol:#fab028e7;

$whiteCol:#FFFFFF;
$darkBlueOpCol: #aea9d8c0;
.allproducts {
  width: 100%;
  height: 82%;

  overflow: hidden;
  overflow-y: scroll;
 
  .view-product-to-edit{
  background: rgba(7, 6, 6, 0.767);
  width: 100%;
  height: 82%;
  position: absolute;
      display: none;
  #close-btn{
    width: 3%;
    height: 25px;
    margin-top: 10px;
    position: absolute;
    right: 1%;
    cursor: pointer;

  }
  .products-box{
   z-index: 5;
  width: 27%;
  height: 435px;
  background: $darkBlueOpCol;
  box-shadow: 0px 4px 8px rgb(209, 205, 205),-8px -8px 8px $darkBlueCol;
  margin-left: 37%;
  margin-top: 50px;
  border-radius: 15%;
  overflow: hidden;
  float: left;
  .box-img{
      width: 100%;
      height: 130px;
      background: $orangeOpCol;
      border-radius: 15%;
      border-bottom: 0.5px solid $darkBlueCol;
      img{
               width: 80%;
      height: 130px;
      text-align: center;
      }
  }
  .box-discription{
      width: 98.5%;
      height: 250px;
      padding-top: 4px;
      overflow: hidden;
      padding-top: 10px;
      #hidden-code-to-compare{
        display: none;
      }
      p{
        margin-left: 5%;
      margin-bottom: 2px;
      font-size: 13px;
      font-weight: bold;

      select,input{
      width: 90%;
            margin-top: 1px;
      margin-bottom: 2px;
      }
      }

  }
  .btn-list{
    width: 95%;
    height: 27px;
    margin-top: 4px;
    border-bottom-left-radius:20%  ;
    border-bottom-right-radius:20%  ;
    align-content: center;
    position: relative;
  
        button{

           width: 25%;
      height: 28px;
      margin-right: 3%;
      background: $orangeCol;
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
      
 
     &::before {
        width: 100%;
        height: 0%;
        background: #4736b1;
        content: "";
        position: absolute;
        top: 50%;
        border-radius: 10%;
        right: 50%;
        z-index: -1;
        transform: translate(50%, -50%);
        transition: 1ms all ease;
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
        color: $orangeCol;
        font-weight: bolder;
          }
        }
        #update-btn{
          margin-left: 18%;
          margin-right: 5%;
          background: $darkBlueCol;
          color: $whiteCol;
          width: 25%;
          height: 25px;
        }
        #delete-btn{
          background: red;
          color: $whiteCol;
                 width: 25%;
          height: 25px;
        }

  }
}
  }

}

</style>
