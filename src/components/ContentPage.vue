<template>
<div>
  <v-container class="noselect" grid-list-md text-xs-center>
    <v-layout row wrap>

      <!--First register-->
      <v-flex xs12>
      <v-layout row wrap justify-space-between style="background-color: #403e3e">
        <v-flex xs12>
          <h3>First register</h3>
        </v-flex> <!--desc-->

        <v-flex  v-for="(num, id) in firstRegister" :key="id">
          <v-card style="min-width: 28px"  hover v-on:click="firstRegister[id].val ^= 1; selectBinaryOperation()" :color="num.val === 1? '#80B12C' : '#BF5030'">
            <v-card-text    class="display-1 px-0 py-2">{{num.val}}</v-card-text>
              <v-divider></v-divider>
            <div style="background-color: #4188D2">{{num.weight}}</div>
          </v-card>
        </v-flex>
        <v-flex xs12 md4>
          <v-card  color="#0D58A6" class="px-0">
            <v-card-text class="display-1 py-2">{{getFirstRegisterValue}} </v-card-text>
            <div style="background-color: #4188D2"> &#8721; </div>
          </v-card>
        </v-flex>
      </v-layout>
      </v-flex>

      <!--Second register-->
      <v-flex xs12 >
        <v-layout row wrap justify-space-between style="background-color: #403e3e">
          <v-flex  xs12>
            <h3>Second register</h3>
          </v-flex> <!--Desc-->
          <v-flex  v-for="(num, id) in secondRegister" :key="id">
            <v-card style="min-width: 28px" hover v-on:click="secondRegister[id].val ^= 1; selectBinaryOperation()" :color="num.val === 1? '#80B12C' : '#BF5030'">
              <v-card-text class="display-1 px-0 py-2">{{num.val}}</v-card-text>
              <v-divider></v-divider>
              <div style="background-color: #4188D2">{{num.weight}}</div>
            </v-card>
          </v-flex>
          <v-flex xs12 md4>
            <v-card  color="#0D58A6" >
              <v-card-text class="display-1 py-2">{{getSecondRegisterValue}} </v-card-text>
              <div style="background-color: #4188D2"> &#8721; </div>
            </v-card>
          </v-flex>
        </v-layout>
      </v-flex>

      <!--Binary operations-->
      <v-flex xs12 mt-4>
        <v-layout xs12 row wrap align-center >
          <v-flex v-for="(item, id) in binaryOperations" :key="id">
            <v-card style="min-width: 34px" :color="item.selected === true? '#619900' : '#8a8a8a'" hover v-on:click="selectOperationButton(id)">
              <v-card-text class="px-0">{{item.code}}</v-card-text>
            </v-card>
          </v-flex>

          <v-flex md3 xs12>
            <v-layout row align-center>
              <v-flex  md6>
                <v-card>
                  <v-card-text > Count: {{operateCount}} </v-card-text>
                </v-card>
              </v-flex>

              <v-flex>
                <v-layout align-start justify-center row fill-height>
                  <v-flex >
                    <v-card style="min-width: 34px"  hover v-on:click="getCount('add'); selectBinaryOperation()">
                      <v-card-text class="px-0">+</v-card-text>
                    </v-card>
                  </v-flex>
                  <v-flex >
                    <v-card style="min-width: 34px"  hover v-on:click="getCount('remove'); selectBinaryOperation()">
                      <v-card-text class="px-0">-</v-card-text>
                    </v-card>
                  </v-flex>

                </v-layout>
              </v-flex>
            </v-layout>
          </v-flex>
        </v-layout>
      </v-flex>


      <!--Result register-->
      <v-flex mt-5 >
          <v-layout row wrap style="background-color: rgb(68,68,68)">
          <v-flex xs12>
            <h1>Result register</h1>
          </v-flex> <!--desc-->

          <v-flex xs12 wrap>
            <v-layout row wrap>
              <v-flex xs12 md8>
                <v-layout wrap row>
                  <!--First register-->
                  <v-flex xs12>
                    <v-layout row>
                      <v-flex v-for="num in getResultFirstByte" :key="num.id">
                        <v-card style="min-width: 28px" :color="num.val === 1? '#80B12C' : '#BF5030'">
                          <v-card-text class="display-1 px-0">{{num.val}}</v-card-text>
                          <v-divider></v-divider>
                          <div class="caption" style="background-color: #4188D2">{{num.weight}}</div>
                        </v-card>
                      </v-flex>
                    </v-layout>
                  </v-flex>

                  <!--Second register-->
                  <v-flex xs12>
                    <v-layout row>
                      <v-flex v-for="num in getResultSecondByte" :key="num.id">
                        <v-card style="min-width: 28px" :color="num.val === 1? '#80B12C' : '#BF5030'">
                          <v-card-text  class="display-1 px-0">{{num.val}}</v-card-text>
                          <v-divider></v-divider>
                          <div class="caption" style="background-color: #4188D2">{{num.weight}}</div>
                        </v-card>
                      </v-flex>
                    </v-layout>
                  </v-flex>
                </v-layout>
              </v-flex>
              <!--Result value-->
              <v-flex d-flex xs12 md4 >
                <v-card class="resultContainer" color="#0D58A6" style="text-align: center;">
                  <v-card-text class="display-1 resultContainer__text">{{resultValue}} </v-card-text>
                  <div class="caption resultContainer__footer" style="background-color: #4188D2"> &#8721; </div>
                </v-card>
              </v-flex>
            </v-layout>
          </v-flex>

        </v-layout>
      </v-flex>
    </v-layout>
  </v-container>
</div>
</template>

<script>
  export default {
    name: "ContentPage",

    data() {
      return {
        //https://colorscheme.ru/#0b320w0w0w0w0
        binaryOperations: [
          {id: 0, name: 'and', selected: true, code: '&'},
          {id: 1, name: 'or', selected: false, code: '|'},
          {id: 2, name: 'Xor', selected: false, code: '^'},
          {id: 3, name: 'not', selected: false, code: '~'},
          {id: 4, name: 'leftShift', selected: false, code: '<<'},
          {id: 5, name: 'rightShift', selected: false, code: '>>'},
          {id: 6, name: 'rightRightShift', selected: false, code: '>>>'},
        ],
        firstRegister: [
          {id: 0, val: 0, weight: 128},
          {id: 1, val: 0, weight: 64},
          {id: 2, val: 0, weight: 32},
          {id: 3, val: 0, weight: 16},
          {id: 4, val: 0, weight: 8},
          {id: 5, val: 0, weight: 4},
          {id: 6, val: 0, weight: 2},
          {id: 7, val: 0, weight: 1},
        ],
        secondRegister: [
          {id: 0, val: 0, weight: 128},
          {id: 1, val: 0, weight: 64},
          {id: 2, val: 0, weight: 32},
          {id: 3, val: 0, weight: 16},
          {id: 4, val: 0, weight: 8},
          {id: 5, val: 0, weight: 4},
          {id: 6, val: 0, weight: 2},
          {id: 7, val: 0, weight: 1},
        ],
        resultRegister: [
          {id: 0, val: 0, weight: '32k'},
          {id: 1, val: 0, weight: '16k'},
          {id: 2, val: 0, weight: 8192},
          {id: 3, val: 0, weight: 4096},
          {id: 4, val: 0, weight: 2048},
          {id: 5, val: 0, weight: 1024},
          {id: 6, val: 0, weight: 512},
          {id: 7, val: 0, weight: 256},
          {id: 8, val: 0, weight: 128},
          {id: 9, val: 0, weight: 64},
          {id: 10, val: 0, weight: 32},
          {id: 11, val: 0, weight: 16},
          {id: 12, val: 0, weight: 8},
          {id: 13, val: 0, weight: 4},
          {id: 14, val: 0, weight: 2},
          {id: 15, val: 0, weight: 1},
        ],
        resultValue: 0,
        operateCount: 1,
        currentOperation: 'and'

      }
    },

    computed: {
      getFirstRegisterValue() {
        let weight = 128;
        let val = 0;
        for (let i = 0; i < this.firstRegister.length; i++) {
          val += weight * this.firstRegister[i].val;
          weight /= 2;
        }
        return val
      },
      getSecondRegisterValue() {
        let weight = 128;
        let val = 0;
        for (let i = 0; i < this.secondRegister.length; i++) {
          val += weight * this.secondRegister[i].val;
          weight /= 2;
        }
        return val
      },
      getResultSecondByte() {
        return this.resultRegister.slice(0, 8);
      },
      getResultFirstByte() {
        return this.resultRegister.slice(8, 17);
      },
    },

    methods: {
      selectBinaryOperation() {
        this.clearResultRegister();
        let firstValue = this.getFirstRegisterValue;
        let secondValue = this.getSecondRegisterValue;

        switch (this.currentOperation) {
          case ('and'): {
            this.binaryAnd(firstValue, secondValue);
            this.getResultRegister()
          }
            break;
          case ('or'): {
            this.binaryOr(firstValue, secondValue);
            this.getResultRegister()
          }
            break;
          case ('Xor'): {
            this.binaryXOr(firstValue, secondValue);
            this.getResultRegister()
          }
            break;
          case ('not'): {
            this.binaryNot(firstValue);
            this.getResultRegister()
          }
            break;
          case ('leftShift'): {
            this.leftShift(firstValue);
            this.getResultRegister()
          }
            break;
          case ('rightShift'): {
            this.rightShift(firstValue);
            this.getResultRegister()
          }
            break;
          case ('rightRightShift'): {
            this.rightRightShift(firstValue);
            this.getResultRegister()
          }
            break;
        }
      },
      selectOperationButton(buttonNum){
        for(let i = 0; i < 7; i++){
          this.binaryOperations[i].selected = false
        }
        this.binaryOperations[buttonNum].selected = true;
        this.currentOperation = this.binaryOperations[buttonNum].name;
        this.selectBinaryOperation();
      },

      binaryAnd(firstValue, secondValue) {
        this.resultValue = firstValue & secondValue;
        /*let val = 0;
        let weight = 128;
        for (let i = 0; i < this.resultRegister.length; i++){
          val += (this.firstRegister[i].val & this.secondRegister[i].val) * weight;
          weight /= 2;
        }
        this.resultValue = val;*/
      },
      binaryOr(firstValue, secondValue) {
        this.resultValue = firstValue | secondValue;
        /*let val = 0;
        let weight = 128;
        for (let i = 0; i < this.resultRegister.length; i++){
          val += (this.firstRegister[i].val | this.secondRegister[i].val) * weight;
          weight /= 2;
        }
        this.resultValue = val;*/
      },
      binaryXOr(firstValue, secondValue) {
        this.resultValue = firstValue ^ secondValue;
      },
      binaryNot(firstValue) {
        //fake js 'not', just for example
        this.resultValue = 65280 - firstValue - 1 + 256
      },
      leftShift(firstValue) {
        this.resultValue = firstValue << this.operateCount;

      },
      rightShift(firstValue) {
        this.resultValue = firstValue >> this.operateCount
        /*let val = 0;
        let weight = 128;
        let flag = true;
        for (let i = 0; i < this.resultRegister.length - 1; i++){
          if (flag && (this.firstRegister[i].val === 1)){
            val += this.firstRegister[i].val * weight; flag = false;
          }
          weight /= (2 * this.operateCount);
          val += (this.firstRegister[i].val) * weight;
        }
        this.resultValue = val;*/
      },
      rightRightShift(firstValue) {
        this.resultValue = firstValue >>> this.operateCount
        /*let val = 0;
        let weight = 128;
        for (let i = 0; i < this.resultRegister.length; i++) {
          weight /= 2;
          val += (this.firstRegister[i].val) * weight;
        }
        this.resultValue = val;*/
      },

      clearResultRegister() {
        for (let i = 0; i < 16; i++) {
          this.resultRegister[i].val = 0;
        }
      },
      getCount(operator) {
        if (operator === 'add') {
          if (this.operateCount > 7) return;
          this.operateCount += 1

        }
        if (operator === 'remove') {
          if (this.operateCount < 2) return;
          this.operateCount -= 1;

        }
      },
      getResultRegister() {
        let val = this.resultValue.toString(2);
        for (let i = val.length - 1; i >= 0; i--) {
          this.resultRegister[16 - val.length + i].val = +val[i];
        }
      }


    },

    watch: {},

    created() {

    }
  }
</script>

<style scoped>
  .noselect {
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -o-user-select: none;
    user-select: none;
  }
  .resultContainer{
    position: relative;
  }
  .resultContainer__footer{
    display: block;
    position: absolute;
    width: 100%;
    bottom: 0px;
    background-color: azure
  }
  .resultContainer__text{
    position: relative;
    top: 50%;    
    transform: translateY(-50%);
  }
</style>
