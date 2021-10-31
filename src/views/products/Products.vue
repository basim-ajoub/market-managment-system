<template>
  <div class="products-views">
    <h1>Products</h1>
    <button id="add-product-btn" class="add-product-btn">
      <router-link to="/addnewproduct">Add New Product</router-link>
    </button>
    <button @click="showFilterBox" class="filter-btn">Filter</button>
    <select name="procuct-filter" id="product-filter">
      <option value="drinks">Drinks</option>
      <option value="foods">Foods</option>
      <option value="cigarettes">Cigarettes</option>
    </select>
    <AllProducts />
  </div>
</template>
<script>
import AllProducts from "../../components/products/allproducs.vue";
export default {
  name: "productsView",
  components: {
    AllProducts,
  },
  methods:{
    showFilterBox:function(){
      document.getElementById("product-filter").style.display="block";
    },
  },
};
</script>
<style lang="scss">
$darkBlueCol: #4736b1;
$greenCol: #56beb0;
$orangeCol: #fba300;
$whiteCol: #ffffff;
.products-views {
  background: $whiteCol;
  height: 100%;
  width: 100%;
  
  overflow: hidden;

  h1 {
    padding-top: 10px;
    margin-left: 1%;
    margin-bottom: 20px;
  }

  #add-product-btn,
  .filter-btn {
    
           width: 12%;
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
      transition: 0.4s all ease;
      float: left;
    a {
      text-decoration: none;
      color: $darkBlueCol;
      border-radius: 10%;
      &:hover{
        color:$whiteCol;
      }
    }
    position: relative;
    z-index: 1;
    &::before {
      width: 100%;
      height: 0%;
      background: $orangeCol;
      content: "";
      position: absolute;
      top: 50%;
      right: 50%;
      z-index: -1;
      transform: translate(50%, -50%);
      transition: 0.6s all ease;
      border-radius: 10%;
    }
    &:hover::before {
      width: 99%;
      height: 100%;
      border-top-left-radius: 40%;
       border-bottom-left-radius: 40%;

    }
    &:hover {
      box-shadow: 0px 0px 1px 1px $orangeCol;
      border: 1.5px solid $orangeCol;
      border-radius: 10%;
      transition: 0.6s ease;

      color: $whiteCol;
      font-weight: bold;
      a {
       
        font-weight: bold;
      }
    }
  }
  #add-product-btn {
    margin-left: 3.8%;
  }
  select {
    margin-left: 0.9%;
    width: 8%;
    height: 24px;
  }
  button{
    float: left;
  }
  .filter-btn{
    
    margin-right: 1%;
  }
  #product-filter{
    display: none;

  }
}
</style>
