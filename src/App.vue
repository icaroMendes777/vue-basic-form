<template>

  <div id="app">

    <HelloWorld msg="V Power!"/>
   
    </p>

    <hr>

    <div class="intro">
    Script básico de validação: validando <i>length, range, option, e display de submit.</i>
    </div>
    
    <hr>
    Nome:
    <input type="text" v-model="name" v-on:change="validateName">
    <div class="error_msg">
    {{nameErrorMessage}}
    </div>

    Idade:
    <input type="text" v-model="age" v-on:change="validateAge" size="4">
    <div class="error_msg">
    {{ageErrorMessage}}
    </div>

    Seu framework preferido:
    <select name="" id="" v-model="framework" v-on:change="validateFramework">
      <option value="react">React</option>
      <option value="angular">Angular</option>
      <option value="vue">Vue</option>
    </select>

    <div class="error_msg" >
    {{frameworkErrorMessage}}
    </div>

<div class="wrap_submit">

 <div v-if="validForm" v-on:click="submit" class="submit">
      Submit
    </div> 
</div>
   
    <button v-on:click="test">test</button>
    
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'


export default {

  
  components: {
    HelloWorld
  },

  updated(){
    if(this.name && this.age && this.framework){
     // console.log('ok')
      if(this.nameErrorMessage 
            || this.ageErrorMessage
            || this.frameworkErrorMessage){
              this.validForm =false
            }else{
              this.validForm =true
            }
    }
  },

  data(){
    return {
       
        name: '',
        nameErrorMessage: '',
        age: '',
        ageErrorMessage: '',
        framework: '',
        frameworkErrorMessage:'',
        validForm: false
      }
  },
  methods: {
    
    test: function()
    {
      alert(this.name)
    },


    validateName: function(){

    this.nameErrorMessage = ""
    let error = false
    if(this.name.length < 2) {
      this.nameErrorMessage = "Nome muito curto, use pelo menos 2 caracteres. "
      error = true
     }
     
     if(this.name.length > 12) {
      this.nameErrorMessage = "Nome muito longo, use no máximo 12 caracteres. "
      error = true
     }

      let pattern = /^[A-Za-záàâãéèêíïóôõöúçñÁÀÂÃÉÈÍÏÓÔÕÖÚÇÑ ]+$/
      if (!pattern.test(this.name)) {
     
      this.nameErrorMessage += "Utilize somente caracteres válidos, sem números e símbolos"
      error = true
    }
    
    if(!error) this.nameErrorMessage = ""

    }, 

    validateAge: function(){

      let error = false;
      this.ageErrorMessage = ""

      if(this.age < 2) {
      this.ageErrorMessage = "Você é muito novo para estar aqui 🧐. "
      error = true
     }
     if(this.age > 120) {
      this.ageErrorMessage = "Certeza que não tem algo errado com a sua idade?🧐. "
      error = true
     }

     let pattern = /^[0-9]+$/
     if (!pattern.test(this.age)) {
      this.ageErrorMessage += "Utilize somente números"
      error = true
    }
    
    if(!error) this.ageErrorMessage = ""

    },
    
    validateFramework()
    {
      if(this.framework != 'vue') 
            this.frameworkErrorMessage = "Sério???"
      else this.frameworkErrorMessage = ""
    },

    submit()
    {
      alert('dados enviados com sucesso')
    }
 
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.intro{
  background-color: #89CFF0;
  padding:2rem;
  margin:1rem;

}

input, select{
  margin:0.5rem;
}

.error_msg{
  font-size:0.7rem;
  color:red;
}
.submit{
  margin:1rem;
  padding:0.6rem;
  border-radius:5px;
  background-color:green;
  color:white;
  width: max-content;
  cursor:pointer;
}
.submit:hover{
  background-color:lightgreen;
}

.wrap_submit{
  margin-top:1rem;
  width:100%;
  display: grid;
  grid-template-columns: auto;
  justify-content:center;
}
</style>
