
<template>
  <div class="container">
    <div class="calc animated bounce delay-1s">
      <div class="container">
        <input class="screen text-right pr-2 my-4" :disabled="true" placeholder="0" :value="sum">
      </div>
      <div class="row mx-1">
        <div class="col-8">
        <button class="btn btn-primary btn-shrt" type="button" @click="concatDigit('M')" >M</button>
        <button class="btn btn-primary btn-shrt" type="button" @click="concatDigit('D')" >D</button>
        <button class="btn btn-primary btn-shrt" type="button" @click="concatDigit('C')" >C</button>
        <button class="btn btn-primary btn-shrt" type="button" @click="concatDigit('L')" >L</button>
        <button class="btn btn-primary btn-shrt" type="button" @click="concatDigit('X')" >X</button>
        <button class="btn btn-primary btn-shrt" type="button" @click="concatDigit('V')" >V</button>
        <button class="btn btn-primary btn-shrt" type="button" @click="concatDigit('I')" >I</button>
        <button class="btn btn-primary btn-shrt" type="button" @click="addition()">+</button>
        </div>
        <div class="col-4">
          <button class="btn btn-lng btn-primary" type="button" @click="reset()" >CE</button>
          <button class="btn btn-lng btn-primary" type="button" @click="final()">=</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  created(){
    this.firstNumber = "";
    this.secondNumber = "";
    this.sum = "";
    this.total = "";
    this.readyToAdd = false;
  },
  computed:{
  },
  methods:{

    concatDigit(digit){
    this.sum = this.sum.concat(digit);
    },

    reset(){
      this.firstNumber = "";
      this.secondNumber = "";
      this.sum = "";
      this.total = "";
      this.readyToAdd = false;
      this.m = "M";
      this.d = "D";
      this.c = "C";
      this.l = "L";
      this.x = "X";
      this.v = "V";
      this.i = "I";
    },

    roman_to_dec(number){
      switch (number){
        case 'M':
          return 1000;
        case 'D':
          return 500;
        case 'C':
          return 100;
        case 'L':
          return 50;
        case 'X':
          return 10;
        case 'V':   
          return 5;
        case 'I':
          return 1;
        default:
          return null;
      }
    },
    
    parse_roman (number) {
      let decNumber = 0;
      let aux1 = 0;
      let aux2 = 0;
      let aux3 = 0;
      let l = number.length;
      for (let i=0; i < l; i++){
        if(i < l){
          aux1 = this.roman_to_dec(number.charAt(i));
          aux2 = this.roman_to_dec(number.charAt(i+1));
          if(aux1 < aux2){
            aux3 = aux2 - aux1;
            decNumber += aux3;
            i++;
          } else {
            decNumber += aux1;
          }
        } else {
          decNumber += parseInt(number.charAt(i));
        }
      }
      return decNumber;
    },

    addition(){
      if (!this.readyToAdd){
        this.readyToAdd = true;
        this.firstNumber = this.parse_roman(this.sum);
        this.sum = "";
      } else {
        this.secondNumber = this.parse_roman(this.sum);
      }
    },

    final(){
      if(this.readyToAdd){
        if (!this.sum){
          alert('You must enter a second number');
        } else {
          this.secondNumber = this.parse_roman(this.sum);
          this.total = this.firstNumber + this.secondNumber;
          this.sum = this.parse_decimal(this.total);
        }
      } else {
        alert('You must enter two numbers to start');
      }
    },

    parse_decimal(number){
      let aux = number.toString();
      let l = aux.length;
      switch(l) {
        case 4: 
          this.total = this.m_to_roman(aux.charAt(0))
                      +this.c_to_roman(aux.charAt(1))
                      +this.d_to_roman(aux.charAt(2))
                      +this.i_to_roman(aux.charAt(3));
          return this.total;
        case 3: 
          this.total = this.c_to_roman(aux.charAt(0))
                      +this.d_to_roman(aux.charAt(1))
                      +this.i_to_roman(aux.charAt(2));
          return this.total;
        case 2:
          this.total = this.d_to_roman(aux.charAt(0))
                      +this.i_to_roman(aux.charAt(1));
          return this.total;
        case 1:
          this.total = this.i_to_roman(aux.charAt(0));
          return this.total;
        default:
          return "";
      }
      
    },

    m_to_roman(a){
      return this.m.repeat(a);
    },

    c_to_roman(a){
      switch(a){
        case '1':
          return this.c;
        case '2':
          return this.c.repeat(2);
        case '3':
          return this.c.repeat(3);
        case '4':
          return this.c+this.d;
        case '5':
          return this.d;
        case '6':
          return this.d+this.c;
        case '7':
          return this.d+this.c.repeat(2);
        case '8':
          return this.d+this.c.repeat(3);
        case '9':
          return this.c+this.m;
        default:
          return "";
      }
    },

    d_to_roman(a){
      switch(a){
        case '1':
          return this.x;
        case '2':
          return this.x.repeat(2);
        case '3':
          return this.x.repeat(3);
        case '4':
          return this.x+this.l;
        case '5':
          return this.l;
        case '6':
          return this.l+this.x;
        case '7':
          return this.x+this.x.repeat(2);
        case '8':
          return this.x+this.x.repeat(3);
        case '9':
          return this.x+this.c;
        default:
          return "";
      }
    },

    i_to_roman(a) {
      switch(a){
        case '1':
          return this.i;
        case '2':
          return this.i.repeat(2);
        case '3':
          return this.i.repeat(3);
        case '4':
          return this.i+this.v;
        case '5':
          return this.v;
        case '6':
          return this.v+this.i;
        case '7':
          return this.v+this.i.repeat(2);
        case '8':
          return this.v+this.i.repeat(3);
        case '9':
          return this.i+this.x;
        default:
          return "";
      }
    }

  },
  data(){
    return {
      sum: "",
      firstNumber: "",
      secondNumber: "",
      total: "",
      readyToAdd: false,
      m: "M",
      d: "D",
      c: "C",
      l: "L",
      x: "X",
      v: "V",
      i: "I"
    }
  }
};

</script>

<style>

</style>
