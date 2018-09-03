<template>
  <div class="calculator">
    <div v-on:mousedown="drag" class="window">Calculator</div>
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn operator">C</div>
    <div @click="sign" class="btn operator">+/-</div>
    <div @click="percent" class="btn operator">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
    data() {
        return {
            previous: null,
            current: '0',
            operator: null,
            operatorClicked: false,
        }
    },
    methods: {

        clear() {
            this.current = '0';
        },

        sign() {
            this.current = this.current.charAt(0) === '-' ?
                this.current.slice(1) : `-${this.current}`;
        },

        percent() {
            this.current = `${parseFloat(this.current) / 100}`;
        },

        append(number) {
            if (this.operatorClicked) {
                this.current = '';
                this.operatorClicked = false;
            }
            this.current = `${this.current}${number}`;
        },

        dot() {
            if (this.current.indexOf('.') === -1) {
                this.append('.');
            }
        },

        setPrevious() {
            this.previous = this.current;
            this.operatorClicked = true;
        },

        divide() {
            this.operator = (a, b) => a / b;
            this.setPrevious();
        },

        times() {
            this.operator = (a, b) => a * b;
            this.setPrevious();
        },

        minus() {
            this.operator = (a, b) => a - b;
            this.setPrevious();
        },

        add() {
            this.operator = (a, b) => a + b;
            this.setPrevious();
        },

        equal() {
            this.current = `${this.operator(
                parseFloat(this.current),
                parseFloat(this.previous)
            )}`;
            this.previous = null;
        },

        drag(e) {
            var calculator = document.querySelector('.calculator');

            var offsetX = e.pageX - calculator.getBoundingClientRect().x;
            var offsetY = e.pageY - calculator.getBoundingClientRect().y;

            document.body.onmousemove =  function(e) {

                calculator.style.left = e.pageX - offsetX + 'px';
                calculator.style.top = e.pageY - offsetY + 'px';

                document.body.addEventListener('mouseup', function() {
                    document.body.onmousemove = null;
                })

            };
        }
    }
}
</script>

<style scoped>
.calculator {
  left: 50px;
  top: 100px;
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  border: 1px solid #008000;
  position: absolute;
}

.display {
  grid-column: 1 / 5;
  background-color: #f2f2f2;
  color: #000;
  padding-right: 10px;
  text-align: right;
}

.window {
  grid-column: 1 / 5;
  background-color: #f2f2f2;
  text-align: left;
  font-size: 0.5em;
  padding: 10px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  background-color: #fff;
  border: 1px solid #f2f2f2;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.btn:hover {
  cursor: default;
}

.btn:not([class~=operator]):hover {
  background-color: #d1d1d1;
}

.btn:not([class~=operator]):active {
  background-color: #8e8e8e;
}

.btn.operator:hover {
  background-color: #008000;
  color: #fff;
}

.btn.operator:active {
  background-color: rgba(0, 173, 0, 0.44);
  color: #fff;
}

.btn.operator {
  background-color: #f9f9f9;
}
</style>
