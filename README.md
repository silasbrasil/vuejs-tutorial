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
Nesse tutorial focaremos em components usando **.vue**. Abaixo é mostrado a estrutura básica de um component vue:

>__BaseComponent.vue__

``` html
<template>
  <div id="root">
  </div>
</template>
<script>
export default {
  name: 'BaseComponent'
}
</script>
<style scoped>
</style>
```

Dessa forma podemos fazer um **import** desse component para utilizá-lo:

>__OtherComponent.vue__

``` html
<template>
  <div id="otherRootComponent">
    <base-component></base-component>
  </div>
</template>
<script>
import BaseComponent from 'path/BaseComponent.vue'

export default {
  name: 'OtherComponent',
  components: {
    'base-component': BaseComponent
  }
}
</script>
<style scoped>
</style>
```

#### Props
Da mesma forma que é possível passar dados para uma tag HTML por meio de suas propriedades como `<input type="text" />` ou `<a href="url"></a>` também é possível criar propriedades para os components vue.

>__PropsComponent.vue__

``` html
<template>
  <div id="root">
    <h3>{{ propName }}</h3>
  </div>
</template>
<script>
export default {
  name: 'ComponentName',
  props: {
    propName: {
      type: String,
      required: true,
      default: 'Texto padrão da prop',
      validatitor: value => value.length > 5
    }
  }
}
</script>
<style scoped>
</style>
```
A prop nomeada de *propName* está definida como String, com valor padrão, sem necessária na hora da utilização do component e ainda tem validação. A documentação do Vue.js define que é essencial declarar os detalhes de uma prop. Ou seja, ao criar um prop coloque o máximo de informação possível para essa propriedade. Isso faz com o que erros de execução sejam lançados.  
Utilizar um component com props:
>__OtherComponent.vue__

``` html
<template>
  <div id="otherRootComponent">
    <props-component propName="Um texto passado na prop"></base-component>
  </div>
</template>
<script>
import PropsComponent from 'path/PropsComponent.vue'

export default {
  name: 'OtherComponent',
  components: {
    'props-component': PropsComponent
  }
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
