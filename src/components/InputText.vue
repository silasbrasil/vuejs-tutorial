<template>
  <input
    id="input"
    :placeholder="myPlaceholder"
    :value="value"
    @input="onType($event.target.value)"/>
</template>

<script>
export default {
  name: 'InputText',
  props: {
    myPlaceholder: {
      type: String,
      default: 'Sem placeholder'
    },
    value: {
      type: String,
      default: ''
    }
  },
  methods: {
    onType(value) {
      this.$emit('input', value)
    }
  }
}
</script>

<style scoped>
#input {
  background-color: azure;
  border: none;
}
</style>