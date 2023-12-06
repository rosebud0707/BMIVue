<template>
  <div>
    <div id="inputArea">
      <h3>BMI計算</h3>
      <p>身長と体重を入力してください。</p>
      <table>
        <tr>
          <th><label for="height">身長：</label></th>
          <input type="number" id="height" v-model="height" @input="checkH" @change="calculateBMI"/>
          <td><label>cm</label></td>
        </tr>
        <tr>
          <th><label for="weight">体重：</label></th>
          <td><input type="number" id="weight" v-model="weight" @input="checkW" @change="calculateBMI"/></td>
          <td><label>kg</label></td>
        </tr>
      </table>
      <div>
        <p v-if="info1 !== null">{{ info1 }}</p>
        <p v-if="info2 !== null">{{ info2 }}</p>
      </div>
      <div v-if="bmi !== null">
        <p>BMI: {{ bmi.toFixed(0) }}</p>
        <p v-if="bmiResult !== ''">結果: {{ bmiResult }}</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      weight: null as number | null,
      height: null as number | null,
      bmi: null as number | null,
      info1: '' as string,
      info2: '' as string,
      bmiResult: '' as string
    };
  },
  methods: {
    checkW() {
      if(this.weight < 0 || this.weight > 600){
        this.bmi = null;
        this.bmiResult = '';
        this.info1 = '0から599kgの間で数値を入力してください。';
        return false;
      } 
      else{
        this.info1 = '';
        return true;
      }
    },
  
    checkH() {
      if(this.height < 0 || this.height > 300){
        this.bmi = null;
        this.bmiResult = '';
        this.info2 = '0から299cmの間で数値を入力してください。';
        return false;
      }
      else{
        this.info2 = '';
        return true;
      }
    },

    calculateBMI() {
      if (this.weight && this.height) {

        if(this.checkH() && this.checkW()){

          const heightInMeters = this.height / 100; // cmをmに変換
          this.bmi = this.weight / (heightInMeters * heightInMeters);

          // BMIの結果を判定
          if (this.bmi < 18.5) {
            this.bmiResult = '低体重（痩せ型）🤔';
          } else if (this.bmi >= 18.5 && this.bmi < 24.9) {
            this.bmiResult = '普通体重🙂';
          } else if (this.bmi >= 25 && this.bmi < 29.9) {
            this.bmiResult = '肥満（１度）🤔';
          } else if (this.bmi >= 30 && this.bmi < 34.9) {
            this.bmiResult = '肥満（２度）🤔';
          } else if (this.bmi >= 35 && this.bmi < 39.9) {
            this.bmiResult = '肥満（３度）😣';
          } else {
            this.bmiResult = '肥満（４度）😣';
          }
        }
      }
      else{
        this.bmi = null;
        this.bmiResult = '';
      }
    }
  },
};
</script>