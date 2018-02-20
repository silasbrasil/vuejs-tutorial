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

#### Props e Validators

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
  name: 'PropsComponent',
  props: {
    propName: {
      type: String,
      required: true,
      default: 'Texto padrão da prop',
      validator: value => value.length > 5
    }
  }
}
</script>
<style scoped>
</style>
```
A prop nomeada de *propName* está definida como String, com valor padrão, sendo necessária na hora da utilização do component e validada. A documentação do Vue.js define que é essencial declarar os detalhes de uma prop. Ou seja, ao criar um prop coloque o máximo de informação possível para essa propriedade. Isso faz com o que erros de execução sejam lançados ainda em desenvolvimento.

Utilizar um component com props:
>__OtherComponent.vue__

``` html
<template>
  <div id="otherRootComponent">
    <props-component propName="Um texto passado na prop"></props-component>
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

#### Events

Da mesma forma que um button em html emite um evento ao ser clicado, podemos emitir eventos quando o nosso componente sofrer alguma alteração ou qualquer outro tipo de mudança.

>__EventComponent.vue__

``` html
<template>
  <input type="text" @input="funcao($event.target.value)">
</template>
<script>
export default {
  name: 'EventComponent',
  methods: {
    funcao (value) {
      this.$emit('onChange', value)
    }
  }
}
</script>
```

Utilizar um component com events:
>__OtherComponent.vue__

``` html
<template>
  <div id="otherComponent">
    <event-component @onChange="doSomething($event)"></event-component>
  </div>
</template>
<script>
import EventComponent from 'path/PropsComponent.vue'

export default {
  name: 'OtherComponent',
  components: {
    'event-component': EventComponent
  },
  methods: {
    doSomething(value) {
      console.log(value)
    }
  }
}
</script>
```

#### v-model

Até agora fizemos os dados irem do componente pai para o filho usando props ou do componente filho para o pai o que chamamos de one-way data flow. No entanto, podemos fazer o two-way data flow, ou seja, fazer os dados fluirem nas duas direções.

Para que isso seja possível usamos o v-model, que é um alias para o evento `@input` e a prop `value`. Dessa forma, qualquer componente que estiver esse comportamento poderá usar a propriedade v-model. Os componentes padrões do html do tipo input, checkbox, radiobutton já tempo esse comportamento por padrão.

>__VModelComponent.vue__

``` html
<template>
  <input type="text" v-model="inputInput">
</template>
<script>
export default {
  name: 'VModelComponent',
  data() {
    return {
      inputInput: ''
    }
  }
}
</script>
```

Podemos mudar o comportamento do v-model da seguinte forma:
>__VModelComponent.vue__

``` html
<template>
  <input type="text" v-model="inputInput">
</template>
<script>
export default {
  model: {
    prop: 'checked',
    event: 'change'
  },
  name: 'VModelComponent',
  data() {
    return {
      inputInput: ''
    }
  }
}
</script>
```
Dessa forma o v-model irá ouvir o evento *change* e a prop *checked*.


#### Slots

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
