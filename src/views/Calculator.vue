<template>
  <v-container>
    <v-row no-gutters justify="center">
      <v-col cols="12">
        <div class="__display rounded_div display-2">0</div>
      </v-col>
    </v-row>

    <div @click="buttonEvent">
    <v-row no-gutters justify="center">
      <v-col cols="12" lg="3">
        <v-btn block
               x-large
               tile
               color="primary"
               class="mx-auto title lighten-2"
               ref="operatorButton"
               v-on:click="isDepressed0 = !isDepressed0"
               :outlined="isDepressed0"
        >+</v-btn>
      </v-col>
      <v-col cols="12" lg="3">
        <v-btn block
               x-large
               tile
               color="primary"
               class="mx-auto title lighten-2"
               ref="operatorButton"
               v-on:click="isDepressed1 = !isDepressed1"
               :outlined="isDepressed1"
        >-</v-btn>
      </v-col>
      <v-col cols="12" lg="3">
        <v-btn block
               x-large
               tile
               color="primary"
               class="mx-auto title lighten-2"
               ref="operatorButton"
               v-on:click="isDepressed2 = !isDepressed2"
               :outlined="isDepressed2"
        >x</v-btn>
      </v-col>
      <v-col cols="12" lg="3">
        <v-btn block
               x-large
               tile
               color="primary"
               class="mx-auto title lighten-2"
               ref="operatorButton"
               v-on:click="isDepressed3 = !isDepressed3"
               :outlined="isDepressed3"
        >÷</v-btn>
      </v-col>
    </v-row>

    <v-row no-gutters>
      <v-col cols="9">
        <v-row no-gutters>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">1</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">2</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">3</v-btn>
          </v-col>
        </v-row>

        <v-row no-gutters justify="center">
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">4</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">5</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">6</v-btn>
          </v-col>
        </v-row>

        <v-row no-gutters justify="center">
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">7</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">8</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">9</v-btn>
          </v-col>
        </v-row>

        <v-row no-gutters justify="center">
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">0</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline">.</v-btn>
          </v-col>
          <v-col cols="4">
            <v-btn block x-large tile class="mx-auto headline" ref="clearButton">{{ clearButtonText.txt }}</v-btn>
          </v-col>
        </v-row>
      </v-col>

      <v-col cols="3">
        <v-row no-gutters>
          <v-col cols="12">
            <v-btn block height="208" width="100" class="display-1">=</v-btn>
          </v-col>
        </v-row>
      </v-col>

    </v-row>
    </div>

  </v-container>
</template>

<script>
  export default {
    name: "Calculator",
    data() {
      return {
        ops: ['+', '-', 'x', '÷'],
        clearButtonText: {
          txt: 'AC'
        },
        isDepressed0: false,
        isDepressed1: false,
        isDepressed2: false,
        isDepressed3: false
      }
    },
    mounted() {
      localStorage.clear()
      // window.createResultString = this.createResultString
      // window.getKeyType = this.getKeyType
      // window.updateCalculatorState = this.updateCalculatorState
    },
    methods: {
      calculate: function (n1, operator, n2) {
        const firstValue = parseFloat(n1)
        const secondValue = parseFloat(n2)
        if (operator === 'add') return firstValue + secondValue
        if (operator === 'subtract') return firstValue - secondValue
        if (operator === 'multiply') return firstValue * secondValue
        if (operator === 'divide') return firstValue / secondValue
      },
      raiseOperators: function () {
        for (let i = 0; i < 4; i++) {
          eval("this.isDepressed" + i.toString() + " = false")
        }
      },
      getKeyType: function (key) {
        if (!isNaN(key)) return 'number'

        if (
          key === '+' ||
          key === '-' ||
          key === 'x' ||
          key === '÷'
        ) return 'operator'

        switch (key) {
          case '=':
            return 'calculate'
          case '.':
            return 'decimal'
          case 'AC':
            return 'clear'
          case 'CE':
            return 'clear'
        }

        return key
      },
      createResultString: function (key, displayedNum) {
        let keyType = this.getKeyType(key)
        let previousKeyType = localStorage.getItem('previousKeyType')

        console.log("Found keyType: ", keyType)
        console.log("Previous KeyType: ", previousKeyType)

        if (keyType === 'number') {
          if (
            displayedNum === '0' ||
            previousKeyType === 'operator' ||
            previousKeyType === 'calculate'
          ) {
            return key
          } else {
            return displayedNum + key
          }
        }

        if (keyType === 'decimal') {
          if (!displayedNum.includes('.')) { return displayedNum + '.' }
          if (previousKeyType === 'operator' || previousKeyType === 'calculate') { return '0.'}
          return displayedNum
        }

        if (keyType === 'operator') {
          const firstValue = localStorage.getItem('firstValue')
          const operator = localStorage.getItem('operator')

          if (
            firstValue &&
            operator &&
            previousKeyType !== 'operator' &&
            previousKeyType !== 'calculate'
          ) {
            return this.calculate(firstValue, operator, displayedNum)
          } else {
            return displayedNum
          }
        }

        if (keyType === 'clear') return 0

        if (keyType === 'calculate') {
          let firstValue = localStorage.getItem('firstValue')
          let operator = localStorage.getItem('operator')
          let secondValue = displayedNum

          if (firstValue) {
            if (previousKeyType === 'calculate') {
              firstValue = displayedNum
              secondValue = localStorage.getItem('modValue')
            }
            return this.calculate(firstValue, operator, secondValue)
          } else {
            return displayedNum
          }
        }
        console.log('ERROR! No matching key type!')
      },
      updateCalculatorState: function (key, calculatedValue, displayedNum) {
        const keyType = this.getKeyType(key)
        localStorage.setItem('previousKeyType', keyType)

        if (keyType === 'operator') {
          switch(key) {
            case '+':
              localStorage.setItem('operator', 'add')
              break
            case '-':
              localStorage.setItem('operator', 'subtract')
              break
            case 'x':
              localStorage.setItem('operator', 'multiply')
              break
            case '÷':
              localStorage.setItem('operator', 'divide')
          }

          if (localStorage.getItem('firstValue') &&
            localStorage.getItem('operator') &&
            localStorage.getItem('previousKeyType') !== 'operator' &&
            localStorage.getItem('previousKeyType') !== 'calculate'
          ) {
            localStorage.setItem('firstValue', calculatedValue)
          } else {
            localStorage.setItem('firstValue', displayedNum)
          }
        }

        if (keyType === 'clear') {
          this.raiseOperators()
          if (key === 'AC') {
            localStorage.setItem('firstValue', '')
            localStorage.setItem('modValue', '')
            localStorage.setItem('operator', '')
            localStorage.setItem('previousKeyType', '')
          } else {
            // TODO: How to update key from here?
            // key.textContent = 'AC'
            this.clearButtonText.txt = 'AC'
          }
        }

        if (keyType !== 'clear') {
          this.clearButtonText.txt = 'CE'
        }

        // Un factored for better readability with localStorage access
        if (keyType === 'calculate') {
          this.raiseOperators()
          let secondValue = displayedNum
          if (localStorage.getItem('firstValue')) {
            if (localStorage.getItem('previousKeyType') === 'calculate') {
              secondValue = localStorage.getItem('modValue')
            }
          }

          localStorage.setItem('modValue', secondValue)
        }
      },
      buttonEvent: function (event) {
        let key = event.target.textContent
        let calcDisplay = document.querySelector('.__display')
        let displayedNum = calcDisplay.textContent
        let resultString = this.createResultString(key, displayedNum)

        calcDisplay.textContent = resultString

        this.updateCalculatorState(key, resultString, displayedNum)
      }
    }
  }
</script>

<style scoped>
.container {
  max-width: 650px;
}
.__display {
  background-color: #222222;
  color: #fff;
  font-size: 1.714285714em;
  padding: 0.5em 0.75em;
  text-align: right;
}

.rounded_div{
  border-radius: 25px 25px 0px 0px;
}
</style>