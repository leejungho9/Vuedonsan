<template>
    <div>
      <img :src="product.image" class="room-img" />
      <h4 @click="$emit('openModal', product.id)">{{product.title}}</h4>
      <p>{{product.price}}원</p>
  </div>

</template>

<script>
export default {
    name : "Card",
    props : {
        product : Object,
        openModal : Boolean,
        clickItem : Number
    }
}
</script>

<style>

</style>