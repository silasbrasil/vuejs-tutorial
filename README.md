# Tutorial de Vue.js

#### Tutorial com as boas práticas de programação usando o Vue.js

##### Nesse tutorial é aplicado os seguinte conceitos:

  - Components (intro)
  - Props
    - Prop definitions
    - Validators
  - Events
  - v-model
    - v-model in custom components
    - Change v-model behavior
  - Slots
    - Named Slots
    - Scoped Slots
  
Os examplos estão em [src/components](https://github.com/silasbrasil/vuejs-tutorial/tree/master/src/components)

#### Components

Os components são formados por três partes: Template, Script e Style. O template é a estrutura do component, script é o comportamento e funcionalidaes e o style é estilo, ou seja, design gráfico do component.

Há duas formas de criar um component Vue.js, usando **vue instance** e usando arquivos **.vue**.
Nesse tutorial focaremos em components usando **.vue**. Como segue:

>__BaseComponent.vue__

``` html
<template>
  <div id="root">
  </div>
</template>
<script>
export default {
  name: 'ComponentName'
}
</script>
<style scoped>
</style>
```

#### Start Dev-Mode

``` bash
# Instala as dependências
npm install

# Roda na porta 8080
npm run dev
```

#### Build Setup

``` bash
# install dependencies
npm install

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```
