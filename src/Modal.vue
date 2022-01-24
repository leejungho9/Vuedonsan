<template>
  <div class="black-bg" v-if="openModal == true">
    <div class="white-bg">
      <h4>{{ products[clickItem].title}}</h4> 
      <img :src="products[clickItem].image" alt="">
      <p>{{ products[clickItem].content}}</p>
      <input v-model.number="month" @keypress="i">
      <p> {{month}}개월 : {{ products[clickItem].price * month}} 원</p>
  <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template> 

<script>
export default {
    name: 'Modal',
    data() {
      return {
        month : "",
      }
    },
    watch : {
      month(a) {
        if(isNaN(a) == true) {
       
          alert("경고")
          this.month = ""
        }
      }
    },
    props : {
        products : Array,
        openModal : Boolean,
        clickItem : Number
    },
    beforeUpdate() {
      if(this.month == 2) {
        alert("최소 3개월부터 계약 가능합니다.")
         this.month = 3
      }
    },

}
</script>

<style>

</style>