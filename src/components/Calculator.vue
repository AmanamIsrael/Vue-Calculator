<template>
<div class="wrapper">
  <div class="calculator">
    <div class="display">{{current || 0}}</div>
    <div @click="clear" class="btn">AC</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="plus" class="btn operator">+</div>
    <div @click="append('0')" class="btn" id="zero">0</div>
    <div @click="dot()" class="btn">.</div>
    <div @click="equals" class="btn operator">=</div>

    </div>
    </div>
</template>

<script>

export default {
  data(){
    return{
      previous : null,
      operatorClicked : false,
      current : '',
      operator : null,
    }
  },
  methods:{

    clear(){
      this.current = '';
    },

    sign(){
    this.current = this.current.charAt(0)==='_'?
    this.current.slice(1) : `-${this.current}`;
  },

  percent(){
    this.current = `${parseFloat(this.current) / 100}`

  },
   

  append(number){
   if(this.operatorClicked){
     this.current='';
     this.operatorClicked = false;
   }
    this.current =`${this.current}${number}`;
  },

  dot(){
    if(this.current.indexOf('.') === -1){
      this.append('.');
    }
  },
  setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
  },
  
  divide(){
     this.operator = (a,b) => a / b;
     this.setPrevious();
     
  },

  minus(){
     this.operator = (a , b) => a - b;
      this.setPrevious();
      console.log(this.operator);
  },

  plus(){
     this.operator = (a , b) => a + b;
      this.setPrevious();
  },

  multiply(){
     this.operator = (a , b) => a * b;
      this.setPrevious();
  },

  equals(){
   
    this.current = `${this.operator(parseFloat(this.current),parseFloat(this.previous))}`;
    this.previous = null;
  } 
},
}
  
</script>
<style scoped>

.calculator{
  font-size: 25px;
  display:grid;
  grid-template-columns: repeat(4 , 1fr);
  grid-auto-columns: minmax(50px, auto);
  width: 18%;
  height:10em;
   margin:0 auto;
   margin-top:10em;
  color:black;
  box-shadow: 0 0 50px 0 gray;

}
.wrapper{
  animation :popIn 5000ms;

}
@keyframes popIn{
  0%,30%{
    transform: scale(0);
    opacity: 0;

  }
  40%,90%{
    opacity:1;
    transform:scale(1);
  }
}

.display{
  width:91.5%;
  grid-column: 1 / 5;
  background-color:rgb(24, 21, 21);
  color: white; 
  text-align: right;
  padding-right: 20px; 
  font-family: poppins;
}
.btn:active{
  background-color: rgb(60, 162, 175);
  transition: all ease .1s;
}
#zero{
  grid-column:1 / 3;
}
.btn{
  background-color:rgb(150, 159, 236);
  border: 1px solid darkcyan;
  cursor:pointer;
  font-family: poppins;
 
  
}
.operator:active{
  background-color:rgb(150, 159, 236);
}
.operator{
  background-color:rgb(226, 69, 142); 
  border: 1px solid darkcyan;
  font-family: consolas;
  font-weight: bold;
  
}

</style>
