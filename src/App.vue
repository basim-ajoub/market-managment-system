<template>
  <div id="app">
     <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap"
      rel="stylesheet"
    />
    <link
      href="https://fonts.googleapis.com/css2?family=Kaushan+Script&display=swap"
      rel="stylesheet"
    />
    <link
      href="https://fonts.googleapis.com/css2?family=Merienda&display=swap"
      rel="stylesheet"
    />
    <link
      href="https://fonts.googleapis.com/css2?family=Luckiest+Guy&display=swap"
      rel="stylesheet"
    />
    <div id="nav">
      <div class="nav-logo-comp">
        <img src="logo.png" alt="logo" />
      </div>
      <div class="nav-elements-comp">
        <ul class="elements-list">
          <li><router-link to="/"> Home</router-link></li>
          <li><router-link to="/sales">Sales</router-link></li>
          <li><router-link to="/products">Products</router-link></li>
          <li><router-link to="/pos">POS</router-link></li>
        </ul>
      </div>
    </div>
    <div id="main-comp">
      <router-view />
    </div>
  </div>
</template>

<style lang="scss">
$darkBlueCol:#4736B1;
$greenCol:#56BEB0;
$orangeCol:#FBA300;
$whiteCol:#FFFFFF;
$permanentFont: "Permanent Marker", cursive;
$kashenFont: "Kaushan Script", cursive;
$meriendaFont: "Merienda", cursive;
$luckiestFont: "Luckiest Guy", cursive;
* {
  padding: 0;
  margin: 0;
  a{
    text-decoration: none;
  }
  
}
#app {
  h1{
    font-family: $luckiestFont; 
  }
  h3{
    font-family:$kashenFont ;
  }
  h4{
    font-family: $meriendaFont;
  }
    button{
      font-family:  $meriendaFont;
      font-weight: bold;
    }
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
width: 100%;
height: 100%;
  color: #2c3e50;
  // start nav componenets

  #nav {

    height: 657px;
    width: 20%;
    background: $darkBlueCol;
background: rgb(58,51,171);
background: linear-gradient(308deg, $darkBlueCol 0%,$darkBlueCol 86%, $greenCol 100%);
font-family: $meriendaFont;

letter-spacing: 1px;
    //start logo components
    .nav-logo-comp {
      width: 100%;
      height: 225px;
      margin-bottom: 20px;
      img {
        width: 80%;
        height: 225px;
        margin-left:5%;
        margin-top: 10px;
        animation-name: moving;
        animation-duration: 10s;
        animation-iteration-count: infinite;
        animation-delay: 0.4s;
        animation-direction: both;
        transition: 0.4s ease-in-out;
      }
      @keyframes moving {
        0%{transform: rotate(0deg);}
        32%{transform: rotate(10deg);}
        67%{transform: rotate(0deg)}
        100%{transform: rotate(-10deg)}
      }
    }
    //end logo components

    //start nav elements components
    .nav-elements-comp {
      width: 100%;
      height: 60%;
      text-align: left;
      .elements-list {
        margin-left: 10%;
        width: 90%;
        list-style: none;
        li {
         
          height: 40px;
          width: 88%;
          margin-bottom: 5px;
           
          
          a{ 
          
           text-align: center;
           justify-items: center;
            width:100%;
            display: inline-block;
            height: 30px;
            position: relative;
            z-index: 1;
            transition: 1s all ease-in-out;
            &::before{
              top: -10px;
              width: 0%;
              left: 20%;
               padding-bottom: 10px;
              height: 90%;
              background: $greenCol;
              content: "";
              position: absolute;
              display: block;
              z-index:-1;
       transform: rotate(15deg);
      
transition: all 0.6s ease-in-out;
            }
            &:hover::before{
              margin-top: 5px;
              margin-left:12%;
              width: 35%;
              
              border-radius: 25%;
               border-bottom-right-radius:85%;
            }

          }
        }
      }
    }
    //end nav elements components
    a {
      font-weight: bold;
      color: $whiteCol;
      text-decoration: none;
      &.router-link-exact-active {
        color: $orangeCol;
      }
    }
  }
  // end nav componenets

  //start main-compenents
  #main-comp {
    width: 80%;
    height: 657px;
    position: absolute;
    top: 0;
    margin-left: 20%;
  }
  //end main-compenents
}
</style>
