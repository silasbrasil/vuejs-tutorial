<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>{{ textInput }}</h3>
    <button @click="limparTextInput">Limpa Text Input</button>
    <div>
      <input-text />

      <input-text myPlaceholder="Com placeholder" /> 

      <input-text
        name="input de texto"
        placeholder="Correta"
        v-model="textInput">
      </input-text>

      <h3>{{ inputText }}</h3>
    </div>
    
    <custom-component :padding="20">
      <h4>Slot sem nome</h4>
      <button slot="footer">Slot no Footer</button>
      <h4 slot="content">Slot content</h4>
    </custom-component>
    
    <list-render :items="meusItems">
      <a slot="list"
        slot-scope="vars">{{ vars.text }} - {{ vars.text2 }}
      </a>
    </list-render>
  </div>
</template>

<script>
import InputText from './InputText'
import Container from './Container'
import ListRender from './ListRender'

export default {
  name: 'HomePage',
  components: {
    'input-text': InputText,
    'custom-component': Container,
    'list-render': ListRender
  },
  data () {
    return {
      msg: 'Que tal esse tutorial de Vue.js?',
      textInput: '',
      inputText: 'v-model running',
      meusItems: [
        'Home',
        'Signup',
        'Signin',
        'About',
        'Contact',
      ]
    }
  },
  methods: {
    limparTextInput () {
      this.textInput = '';
    }
  }
}
</script>

<style scoped>
h1 {
  font-weight: normal;
}
  
  a {
    display: block;
  }
</style>
