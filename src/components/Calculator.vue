<template>
  <div class='calculator'>
    <div class="display">{{ current || '0'}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="apppend('7')" class="btn">7</div>
    <div @click="apppend('8')" class="btn">8</div>
    <div @click="apppend('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="apppend('4')" class="btn">4</div>
    <div @click="apppend('5')" class="btn">5</div>
    <div @click="apppend('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="apppend('1')" class="btn">1</div>
    <div @click="apppend('2')" class="btn">2</div>
    <div @click="apppend('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="apppend('0')" class="btn zero">0</div>
    <div @click="dot()" class="btn">.</div> 
    <div @click="equal" class="btn">=</div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      current:'',
      operator: null,
      previous:null,
      operatorClicked:false
    }
  },
  methods:{
    clear(){
      this.current = ''
    },
    sign(){
      this.current = this.current.charAt(0) === '-'?
       this.current.slice(1): `-${this.current}`;
    },
    percent(){
      this.current = `${parseFloat(this.current) / 100}`;
    },
    apppend(number){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false
      }
      this.current = `${this.current}${number}`
    },
    dot(){
      if(this.current.indexOf('.') === -1){
        this.apppend('.')
      }
    },
    divide(){
      this.operator = (a, b) => a / b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    add(){
      this.operator = (a, b) => a + b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    minus(){
      this.operator = (a, b) => a - b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    times(){
      this.operator = (a, b) => a * b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    equal(){
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator{
    margin:0 auto;
    width:400px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
  }
  .display{
    grid-column: 1 / 5;
    background-color: rgb(107, 155, 139);
  }
  .zero{
    grid-column: 1 / 3;
  }
  .btn{
    background-color: burlywood;
    border: 1px solid black;
  }
  .operator{
    background-color: orange;
    color: white;
  }
</style>
