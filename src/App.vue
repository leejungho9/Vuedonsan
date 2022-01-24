<template>

<transition name="fade">
  <Modal @closeModal ="openModal = false" :products = "products" :clickItem = "clickItem" :openModal = "openModal" />
</transition>

<!-- 메뉴 -->
  <div class="menu">
    <a v-for="menu in menus" :key="menu">
      {{menu}}</a>
  </div>

<Discount v-if="showDiscount == true"  :discount = "discount"/>

<div>
  <span>정렬 : </span>
  <select id="num" @change="select()">
    <option value="priceSort">----</option>
    <option value="priceSort" >가격순정렬</option>
    <option value="sortBack">처음으로</option>
  </select>
</div>

<div class="card-container">
  <Card @openModal= "openModal = true; clickItem= $event"  v-for="(product, i) in products" :key="product" :product="products[i]"/>
</div>

</template>

<script>

import product from './post.js'
import Discount from './Discount.vue'
import Modal from './Modal.vue'
import Card from './Card.vue'

export default {
  name: 'App',

  data() {
    return {
      menus : ['Home','Shop','About'],
      originalproducts : [...product],
      products : product,
      openModal : false,
      clickItem : 0,
      reportCounts : [0, 0, 0],
      showDiscount : true,
      discount : 30

    }
  },
  methods : {
    increase() {
      this.reportCounts[0]+=1;
    },
    priceSort() {
      this.products.sort(function(a,b) {
        return a.price - b.price
      })
    },
    sortBack() {
      this.products = [...this.originalproducts];
    },
    select() {
      let seleted = document.getElementById("num")
      var selectValue = seleted.options[seleted.selectedIndex].value;
      console.log(selectValue)
      if(selectValue == "priceSort") {
        this.priceSort()
      } else if(selectValue == "sortBack") {
        this.sortBack();
      }
       
    }
  },
  mounted() {
    var a = setInterval(()=> {
          this.discount = this.discount - 1;
          if(this.discount == 0) {
            clearInterval(a)
          }
    }, 1000);
  },
  update() {

  },
  components: {
   Discount,
   Modal,
   Card
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

}

.menu {
  background-color: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color : white;
  padding: 10px;
}
.room-img {
  width : 400px;
  margin-top: 40px;
}
body{
  margin : 0
}
div { 
  box-sizing: border-box;
}
.black-bg{
  width:100%;
  height: 100%;
  background-color : reba(0,0,0,0.5);
  position: fixed; 
  padding : 20px;
}
.white-bg{
  width:100%;
  height: 600px;
  background-color : #fff;
  border-radius: 8px;
  padding: 20px;

}
.white-bg img {
  width : 500px;
  height: 300px;
}
.discount{
  background-color: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
.start {
  opacity: 0;
  transition : all 1s;
}
.end {
  opacity: 1;
}
.fade-enter-from {
  transform:  translateY(-1000px);
  }
.fade-enter-active{ 
  transition: 1s;
}
.fade-enter-to {opacity: 1;}

.fade-leave-from {
  opacity: 1
  }
.fade-leave-active{ 
  transition: 1s;
}
.fade-leave-to {
  transform: translateY(+2000px);
}
.card-container {
     display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
}
.card-container  div {
  padding: 0 10px;
}
</style>
