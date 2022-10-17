<template>
  <div id="app">
    <input type="number" v-model="num1" />
    <input type="number" v-model="num2" />
    <p>result: {{ result }}</p>

    <div>
      <button v-on:click="calculate">+</button>
      <button v-on:click="calculate">-</button>
      <button v-on:click="calculate">*</button>
      <button v-on:click="calculate">/</button>
      <button v-on:click="calculate">x^y</button>
      <button v-on:click="calculate">x_y</button>
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
    }
  },
  methods: {
    calculate(e) {
      const action = e.target.textContent
      const num1 = Number(this.num1)
      const num2 = Number(this.num2)
      switch (action) {
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
  },
}
</script>

<style lang="scss"></style>
