<template>
  <div class="containerList">
    <slot name="list"
          v-for="item in items"
          :text="item"
          text2="sssss" >
    </slot>
  </div>
</template>

<script>
export default {
  name: 'ListRender',
  props: {
    items: {
      type: Array,
      default: []
    }
  }
}
</script>

<style scoped>
.containerList {
  background-color: beige;
  width: 100%;
  height: auto;
}
</style>