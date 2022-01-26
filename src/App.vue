<template>
<!--  <div id="app">-->
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
<!--    <HelloWorld msg="приветики"/>-->
<!--  </div>-->
  <div>
    <div class="display">
      <input v-model.number="operand1"/>
      <input v-model.number="operand2"/>
      = {{result}}
    </div>
    <div class="keyboard">
      <button v-on:click="calculate ('+')">+</button>
      <button v-on:click="calculate ('-')">-</button>
      <button @click="calculate ('/')">/</button>
      <button @click="calculate ('*')">*</button>
      <button @click="calculate ('entire')">entire /</button>
      <button @click="calculate ('^')">^</button>
    </div>
    <div v-if="error">ошибка! {{error}} </div>
    <div class="strange-message">
      <template v-if="result < 0">Получилось отрицательное число</template>
      <template v-else-if="result < 100"> Результат в первой сотне</template>
      <template v-else> Получилось слишком большое число</template>
    </div>
  </div>
</template>

<script>
//
// import HelloWorld from './components/HelloWorld.vue'

// export default {
//   name: 'App',
//   components: {
//     HelloWorld
//   }
// }
export default {
  name: 'Calculator',
  data(){
    return {
      operand1: 0,
      operand2: 0,
      result: 0,
      error: ''
    }
  },
  methods: {
    add() {
      this.result = this.operand1 + this.operand2
    },
    substract (){
      this.result = this.operand1 - this.operand2
    },
    divide (){
      const { operand1, operand2} = this
      if (operand2 == 0) {
        this.error = 'на 0 делить нельзя!'
      } else {
        this.result =operand1 / operand2
      }
    },
    multiply () {
      this.result = this.operand1 * this.operand2
    },
    entireDivide (){
      this.result = Math.floor(this.operand1 / this.operand2)
    },
    degree () {
      this.result = Math.pow (this.operand1, this.operand2)
    },
    calculate (operation = "+") {
      this.error =''
      switch (operation) {
        case "+":
          this.add()
          break;
        case "-":
          this.substract()
          break;
        case "/":
          this.divide()
          break;
        case "*":
          this.multiply()
          break;
        case "entire":
          this.entireDivide()
          break;
        case "^":
          this.degree()
          break;
      }
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
</style>
