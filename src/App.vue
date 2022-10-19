<template>
  <div id="app">
    <input type="number" v-model="num1" />
    <input type="number" v-model="num2" />
    <p>result: {{ result }}</p>
    <div>
      <button
        v-for="(operation, index) of operations"
        :key="index"
        v-on:click="calculate(index)"
      >
        {{ operation }}
      </button>
    </div>
    <div class="keyboard-box">
      <input
        type="checkbox"
        name="keyboard-checkbox"
        id="keyboard-checkbox"
        v-model="showBox"
      />
      <label for="keyboard-checkbox">
        Показать/Скрыть экранную клавиатуру</label
      >
      <div class="keyboard" v-show="showBox">
        <button
          v-for="(item, index) of keyboard"
          :key="item + index"
          v-on:click="inputNum(item)"
        >
          {{ item }}
        </button>
        <div>
          <input
            type="radio"
            v-model="radioPicked"
            name="radios"
            value="1"
            id="num1"
          />
          <label for="num1"> Операнд 1</label>
          <input
            type="radio"
            v-model="radioPicked"
            name="radios"
            value="2"
            id="num2"
          /><label for="num2"> Операнд 2</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      num1: 0,
      num2: 0,
      result: 0,
      operations: ['+', '-', '*', '/', 'x^y', 'x_y'],
      showBox: false,
      keyboard: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'del'],
      radioPicked: '',
    }
  },
  methods: {
    calculate(index) {
      const num1 = Number(this.num1)
      const num2 = Number(this.num2)
      switch (this.operations[index]) {
        case '+':
          this.result = num1 + num2
          break
        case '-':
          this.result = num1 - num2
          break
        case '*':
          this.result = num1 * num2
          break
        case '/':
          this.result = num1 / num2
          break
        case 'x^y':
          this.result = num1 ** num2
          break
        case 'x_y':
          this.result = Math.floor(num1 / num2)
          break
      }
    },
    inputNum(e) {
      if (e != 'del') {
        if (this.radioPicked == 1) {
          this.num1 += e
          if (this.num1.length > 1 && this.num1[0] == 0) {
            this.num1 = this.num1.slice(1)
          }
        }
        if (this.radioPicked == 2) {
          this.num2 += e
          if (this.num2.length > 1 && this.num2[0] == 0) {
            this.num2 = this.num2.slice(1)
          }
        }
      } else {
        this.radioPicked == 1
          ? (this.num1 = this.num1.slice(0, -1))
          : this.radioPicked == 2
          ? (this.num2 = this.num2.slice(0, -1))
          : console.log('error')

        this.num1 === ''
          ? (this.num1 = 0)
          : this.num2 === ''
          ? (this.num2 = 0)
          : ''
      }
    },
  },
}
</script>

<style lang="scss"></style>
