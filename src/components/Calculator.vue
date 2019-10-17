<template>
    <div class="calculator">
        <div class="display">{{ current || '0' }}</div>

        <div @click="clear" class="btn">C</div>
        <div @click="sign" class="btn">&#177;</div>
        <div @click="percent" class="btn">%</div>
        <div @click="divide" class="btn btn-special">&#xF7;</div>

        <div @click="append('7')" class="btn">7</div>
        <div @click="append('8')" class="btn">8</div>
        <div @click="append('9')" class="btn">9</div>
        <div @click="times" class="btn btn-special">x</div>

        <div @click="append('4')" class="btn">4</div>
        <div @click="append('5')" class="btn">5</div>
        <div @click="append('6')" class="btn">6</div>
        <div @click="minus" class="btn btn-special">-</div>

        <div @click="append('1')" class="btn">1</div>
        <div @click="append('2')" class="btn">2</div>
        <div @click="append('3')" class="btn">3</div>
        <div @click="add" class="btn btn-special">+</div>

        <div @click="append('0')" class="zero btn">0</div>
        <div @click="dot" class="btn">.</div>
        <div @click="equals" class="btn btn-special">=</div>
    </div>
</template>

<script>
    export default {
        name: 'HelloWorld',
        data() {
            return {
                current: '',
                previous: null,
                operator: null,
                operatorClicked: false
            }
        },
        methods: {
            clear() {
                this.current = ''
            },
            sign() {
                this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
            },
            percent() {
                this.current = `${parseFloat(this.current) / 100}`
            },
            append(num) {
                if (this.operatorClicked){
                    this.current = '';
                    this.operatorClicked = false;
                }
                this.current = `${this.current}${num}`
            },
            dot() {
                if (this.current.indexOf('.') === -1) {
                    this.append('.')
                }
            },
            setPrevious() {
                this.previous = this.current;
                this.operatorClicked = true
            },
            divide() {
                this.operator = (a, b) => a / b;
                this.setPrevious()
            },
            add() {
                this.operator = (a, b) => a + b;
                this.setPrevious()
            },
            minus() {
                this.operator = (a, b) => a - b;
                this.setPrevious()
            },
            times() {
                this.operator = (a, b) => a * b;
                this.setPrevious()
            },
            equals() {
                this.current = `${this.operator(parseFloat(this.current), parseFloat(this.previous))}`;
                this.previous = null
            }
        }
    }
</script>

<style scoped>
    .calculator {
        width: 300px;
        margin: 0 auto;
        font-weight: lighter;
        font-size: 40px;
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-auto-rows: minmax(50px, auto);
    }

    .display {
        background-color: #333;
        grid-column: 1 / 5;
        color: #fff;
        text-align: right;
        padding-right: 10px;
    }

    .zero {
        grid-column: 1 / 3;
    }

    .btn {
        background-color: #eeeeee;
        border: 1px solid #888;
    }

    .btn-special {
        background-color: #eda700;
        color: #ffffff;
    }
</style>
