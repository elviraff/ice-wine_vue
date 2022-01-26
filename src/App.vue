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
      <button v-for="operand in operands"
              v-bind:key="operand"
              v-bind:title="operand"
              v-bind:disabled="operand1 == '' || operand2 == ''"
              @click="calculate(operand)">
        {{operand}}
      </button>
    </div>
    <div v-if="error">ошибка! {{error}} </div>
    <div class="strange-message">
      <template v-if="result < 0">Получилось отрицательное число</template>
      <template v-else-if="result < 100"> Результат в первой сотне</template>
      <template v-else> Получилось слишком большое число</template>
    </div>
    <br>
    <input v-model="keyboardActivated" type="checkbox" id="activateBoard">
    <label for="activateBoard"> Activate if e-keyboard is needed</label>
    <br>
    <button v-for="keyItem in keyboard"
      v-bind:key="keyItem"
      v-bind:disabled="keyboardActivated == false"
      @click="writeKey(keyItem)">
      {{keyItem}}
    </button>
    <br>
    <input type="radio" name="selectOperand" value="first" v-model="pickedOperand" id="pickedOperand1">
    <label for="pickedOperand1"> Operand 1</label>
    <input type="radio" name="selectOperand" value="second" v-model="pickedOperand" id="pickedOperand2">
    <label for="pickedOperand2"> Operand 2</label>
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
let keyResult1 = '';
let keyResult2 = '';
export default {
  name: 'Calculator',
  data(){
    return {
      operands: ['+', '-', '/', '*', 'entire', '^'],
      operand1: '',
      operand2: 0,
      result: 0,
      error: '',
      keyboard: ['0','1','2','3','4','5','6','7','8','9','<--'],
      keyboardActivated: false,
      pickedOperand:'',
    }
  },
  methods: {
    add() {
      this.result = +this.operand1 + +this.operand2
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
    },
    writeKey (keyValue){
      if (this.pickedOperand == 'first') {
        if (keyValue == '<--'){
          keyResult1 = Math.floor(keyResult1 / 10);
          this.operand1 = keyResult1
        } else {
          keyResult1 += keyValue;
          this.operand1 = keyResult1
        }
      }
      else if (this.pickedOperand == 'second'){
        if (keyValue == '<--') {
          keyResult2 = Math.floor(keyResult2 / 10);
          this.operand2 = keyResult2
        } else {
          keyResult2 += keyValue;
          this.operand2 = keyResult2
        }
      }
      },
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
