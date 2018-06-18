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
import axios from 'axios'

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
  created() {
    this.getImageMetaData()
  },
  methods: {
    limparTextInput () {
      this.textInput = '';
    },
    getImageMetaData() {
      const urlImage = 'https://semantic-ui.com/images/avatar2/large/elyse.png'
      axios.get(urlImage, { responseType: 'blob' })
        .then(response => {
          console.log(response.data)
        })
      // console.log(img.filesize)
    },
    testSerialPromises() {
      let promiseArray = [
        axios.get('https://reqres.in/api/users/1').then(result => result.data.data),
        axios.get('https://reqres.in/api/users/2').then(result => result.data.data),
        axios.get('https://reqres.in/api/users/3').then(result => result.data.data),
        axios.get('https://reqres.in/api/users/4').then(result => result.data.data),
        axios.get('https://reqres.in/api/users/5').then(result => result.data.data),
        axios.get('https://reqres.in/api/users/6').then(result => result.data.data)
      ]

      const promiseSerial = promisesList =>
        promisesList.reduce((oldPromise, currPromise) => {
          return oldPromise.then(dataFromAxios => {
            console.log(dataFromAxios)
            return currPromise.then()
          })
        }, Promise.resolve())

      promiseSerial(promiseArray)
        .then(result => {
          console.log('FIM', result)
        })
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
