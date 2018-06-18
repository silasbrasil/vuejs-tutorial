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
    this.downloadProgress()
  },
  methods: {
    limparTextInput () {
      this.textInput = '';
    },
    downloadProgress() {
      const urlImage = 'https://semantic-ui.com/images/avatar2/large/elyse.png'
      const url4KImage = 'https://images.unsplash.com/photo-1494249465471-5655b7878482?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=191559dc1cae3f8967d568dfd8a77093&auto=format&fit=crop&w=1350&q=80'
      this.getImageByStream(url4KImage)

      const urlJson = 'https://reqres.in/api/users/1'
      // this.getJsonByStream(urlJson)
      // this.getJsonByStream(urlJson)
    },
    getJsonByStream(url, on, end, error) {
      const oReq = new XMLHttpRequest()
      oReq.open('GET', url, true)
      oReq.responseType = "arraybuffer"

      console.log('CHAMOU')

      oReq.onload = event => {
        let arrayBuffer = oReq.response // Note: not oReq.responseText
        let stringResult = ''
        if (arrayBuffer) {
          let byteArray = new Uint8Array(arrayBuffer)
          let total = 0
          let lastResult = 0
          for (total = 0; total < byteArray.byteLength; total++) {
            if ((lastResult + 10) <= total) {
              lastResult = total
              // console.log('bytes baixados: ', lastResult)
            }
            stringResult = String.fromCharCode.apply(String, byteArray)
          }
          // console.log('Download JSON finalizado')
          // console.log('Total: ', total)
          // console.log(JSON.parse(stringResult).data)
        }
      }

      oReq.onprogress = event => {
        console.log(event)
        if (event.lengthComputable) {
          console.log(event.loaded, event.total)
          const percentComplete = event.loaded / event.total * 100;
          console.log(percentComplete)
        }
      }

      oReq.onloadend = event => {
        console.log('finished')
      }

      oReq.send(null);
    },
    getImageByStream(imageUrl) {
      const oReq = new XMLHttpRequest()
      oReq.open('GET', imageUrl, true)
      oReq.responseType = "arraybuffer"

      oReq.onload = event => {
        let arrayBuffer = oReq.response
        if (arrayBuffer) {
          const byteArray = new Uint8Array(arrayBuffer)
          let total = 0
          let lastResult = 0
          for (total = 0; total < byteArray.byteLength; total++) {
            if ((lastResult + 10) <= total) {
              lastResult = total
              // console.log('bytes baixados: ', lastResult)
            }
          }
          // console.log('Download Image finalizado')
          // console.log('Total: ', total)
        }
      }

      oReq.onprogress = event => {
        // console.log(event)
        if (event.lengthComputable) {
          // console.log(event.loaded, event.total)
          const percentComplete = event.loaded / event.total * 100;
          console.log(percentComplete)
        }
      }

      oReq.send()
    },
    getImageMetaData() {
      const urlImage = 'https://semantic-ui.com/images/avatar2/large/elyse.png'
      axios.get(urlImage, { responseType: 'blob' })
        .then(response => {
          console.log(response.data)
        })
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
