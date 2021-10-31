<template>
  <div  class="products-box">
     
    <div  id="box-img" class="box-img">
     
<img :src="producttype+'.png'" alt="">
   
     	
    </div>
    <div class="box-discription">
        <p>Name : <span id="name-field">{{productname}}</span></p>
        <p >Type : <span id="type-field">{{producttype}}</span></p>  <p>Price : <span id="prise-field">{{productprise}} $</span></p>
        <p id="float">Quantity : <span id="quantity-field">{{productquantity}}</span></p><p>Size : <span id="size-field">{{productsize}}</span></p>
         <p>Status : <span> {{availaility}}</span>  </p>
          <p>Code : <span id="code-field">{{productcode}}</span></p>
    </div>
          <div class="btn-list">
            <button @click="viewProduct" id="edit-btn">Edit</button>
            <button @click="deleteProduct" id="delete-btn">Delete</button>
          </div>
  </div>
</template>
<script>
export default {
  name: "productBoxComp",
  
data:function(){
return{
  availaility:"",
}
},
mounted:function(){
  this.checkAvailability();
},

  props:["productname","productprise","productsize","productcode","producttype","productquantity","producticon"],
methods:{
 
  deleteProduct:function(){
    console.log("deleted" + this.productname);
      for(let i=1 ; i<localStorage.length+100;i++){
         var productInfoKey = "productInfoKey" + i;
if(localStorage.getItem(productInfoKey) != null){
       var retriveProductValue = JSON.parse(localStorage.getItem(productInfoKey));
if( retriveProductValue.productcode == this.productcode){
 localStorage.removeItem(productInfoKey);
    console.log('This Product : '+ this.productname +' Is Deleted');
        location.reload();
}
}
    }
  },
    viewProduct:function(){
      
    document.getElementById("view-product-to-edit").style.display = "block";
    document.getElementById("edit-add-products-type").value = this.producttype;
    document.getElementById("edit-name-field").value = this.productname;
    document.getElementById("edit-price-field").value = this.productprise;
       document.getElementById("edit-size-field").value = this.productsize;
    document.getElementById("edit-quantity-field").value = this.productquantity;
       document.getElementById("edit-code-field").value = this.productcode;
       document.getElementById("hidden-code-to-compare").innerText = this.productcode;//hidden to get the product from local storage

  },
  checkAvailability:function(){
    if(this.productquantity <=0){
      this.availaility = "Not Available";
    }
    else{
      this.availaility = "Available";
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
.products-box {
  width: 215px;
  height: 322px;
  background: $darkBlueOpCol;
  box-shadow: 0px 4px 8px rgb(209, 205, 205),-8px -8px 8px $darkBlueCol;
  margin-left: 4%;
  margin-top: 20px;
  border-radius: 15%;
  overflow: hidden;
  float: left;
  .box-img{
      width: 100%;
      height: 150px;
      background: $orangeOpCol;
      border-radius: 15%;
      border-bottom: 0.5px solid $darkBlueCol;

      img{
        margin-top: 20px;
        width: 80%;
        margin-left: 9%;
        height: 110px;
       
      }

  }
  .box-discription{
      width: 98.5%;
  
      height: 125px;
      padding-top: 4px;
      overflow: hidden;
      border-radius: 15%;

      p{
        margin-left: 5%;
      margin-bottom: 2px;
      font-size: 13px;
      font-weight: bold;
      span{
        font-size: 14px;
        font-weight: bolder;
      }
      }
      #float{
        float: left;
        margin-right: 7.5%;
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
          margin-top: 5px;
          width: 30%;
          height: 21px;
          border: 1px solid $darkBlueCol;
          border-radius: 12%;
          color: $whiteCol;
          cursor: pointer;
          transition: 0.1s ease-in-out;
          &:hover{
            width: 32%;
            height: 21.5px ;
            box-shadow: 0px 4px 5px $whiteCol;
          }
        }
        #edit-btn{
          margin-left: 18%;
          margin-right: 5%;
          background: $darkBlueCol;
        }
        #delete-btn{
          opacity: 0.7;
          background: rgba(255, 0, 0, 0.863);
          &:hover{
            opacity: 1;
          }
        }

  }
}
</style>
