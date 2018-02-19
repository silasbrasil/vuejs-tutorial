<template>
  <div :class="classOptions">
    <slot></slot>
    <slot name="content"></slot>
    <slot name="footer"></slot>
  </div>
</template>

<script>
export default {
  name: 'CustomContainer',
  props: {
    padding: {
      type: Number,
      default: 10,
      validator: value =>
        [10, 20, 30, 40, 50].indexOf(value) !== -1
    }
  },
  data() {
    return {
      classOptions: {
        'container': true,
        'padding-10': this.padding === 10,
        'padding-20': this.padding === 20,
        'padding-30': this.padding === 30
      }
    }
  }
}
</script>

<style scoped>
.container {
  background-color: azure;
  width: 100%;
  height: auto;
}

.padding-10 {
  padding: 10px;
}
  
.padding-20 {
  padding: 20px;
}

.padding-30 {
  padding: 30px;
}
</style>