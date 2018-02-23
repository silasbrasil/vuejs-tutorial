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
  model: {
    prop: 'checked',
    event: 'change'
  },
  props: {
    myPlaceholder: {
      type: String,
      default: 'Sem placeholder'
    },
    value: {
      type: String,
      default: ''
    },
    checked: String,
  },
  methods: {
    onType(value) {
      this.$emit('input', value)
      this.$emit('change', value)
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