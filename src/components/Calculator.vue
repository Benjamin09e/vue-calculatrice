<script>
export default {
  name: 'Calculator',
  props: {
    msg: String
  },

  data() {
    return {
      calculatorValue: '',
      calculatorElements: ['C','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.','=','AC'],
      operator: null,
      previousCalculatorValue: '',
    }
  },

  methods: {
    action(n){

      /* ajouter des valeurs*/
      if(!isNaN(n) || n === '.'){
        this.calculatorValue += n + '';
      }

      /* effacer des valeurs */
      if(n === 'C'){
        this.calculatorValue = '';
      }

      /*  calcul du pourcentage */
      if(n === '%'){
        this.calculatorValue = this.calculatorValue / 100 + '';
      }

      /* Les operateurs */
      if(['/','*','-','+', 'AC'].includes(n)){
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = '';
      }

      /* Calcul le resultat avec la function eval */
      if(n === '='){
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.previousCalculatorValue = '';
        this.operator = null;
      }
    }
  }
}
</script>


<template>
  <div class="p-1" style="max-width: 400px; margin: 200px auto; background: #efefef">
    <!-- Calcul  le resultat -->
    <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-dark">
      {{ calculatorValue || 0 }}
    </div>
    <!-- buttons calculatrice -->
    <div class="row no-gutters">
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class="{'bg-vue-green': ['C','*','/','-','+','%','=','AC'].includes(n)}"
          @click="action(n)">
          {{n}}
        </div>
      </div>
    </div>
  </div>
</template>


<style scoped>
  .bg-vue-dark {
    background: #310d0d;
  }
  .hover-class:hover {
    cursor: pointer;
    background: #1d632fc0;
  }
  .bg-vue-green {
    background: orange;
  }
</style>
