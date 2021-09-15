<template>
  <div class="container pt-5">
    <table>
      <tr>
        <td>
          <span >الجنس</span>
        </td>
        <td>
          <input type="radio" id="female" checked="checked" name="Gender" v-on:click="Female()">امرأة
          <input type="radio" id="male" name="Gender" v-on:click="Male()"> رجل
        </td>
      </tr>
      <tr>
        <td>
          <span>الوزن</span>
        </td>
        <td>
          <input type="text" id="weight" value="" v-on:keyup="check()">كجم
        </td>
      </tr>
      <tr>
        <td>
          <span>الطول</span>
        </td>
        <td>
          <input type="text" id="height" value="" v-on:keyup="check()">سم
        </td>
      </tr>
      <tr>
        <td colspan="2"><strong>المقاسات:</strong></td>
      </tr>
      <tr>
        <td>
          <span>الرقبة</span>
        </td>
        <td>
          <input type="text" value="" id="neck" v-on:keyup="check()">سم
        </td>
      </tr>
      <tr>
        <td>
          <span>الوسط</span>
        </td>
        <td>
          <input type="text" value="" id="abdomen" v-on:keyup="check()">سم
        </td>
      </tr>
      <tr id="hiprow">
        <td>
          <span>المؤخرة</span>
        </td>
        <td>
          <input type="text" value="" id="hip" v-on:keyup="check()">سم
        </td>
      </tr>
      <tr class="result">
        <td>نسبة الدهون</td>
        <td id="BodyFat">0 %</td>
      </tr>
      <tr class="result">
        <td>وزن الدهون</td>
        <td id="FatMass">0 كجم</td>
      </tr>
      <tr class="result">
        <td>وزن الكتلة اللادهنية</td>
        <td id="LeanMass">0 كجم</td>
      </tr>
      <tr class="result">
        <td>فئة الدهون</td>
        <td id="bfc">Acceptable</td>
      </tr>
    </table>
  </div>
</template>

<script>
  export default {
    methods: {
      Male() {
          document.getElementById("hiprow").setAttribute("style", "visibility: hidden");
          this.check();
      },
      Female() {
          document.getElementById("hiprow").setAttribute("style", "visibility: visible");
          this.check();
      },
      check() {
        let bodyFat = document.getElementById("BodyFat");
        let fatMass = document.getElementById("FatMass");
        let leanMass = document.getElementById("LeanMass");
        let bfc = document.getElementById("bfc");
        bodyFat.innerHTML = "";
        fatMass.innerHTML = "";
        leanMass.innerHTML = "";
        bfc.innerHTML = "";
        if (document.getElementById("female").checked) {
            let bfFemale = Math.round(495 / (1.29579 - .35004 * this.log10(parseInt(document.getElementById("abdomen").value) + parseInt(document.getElementById("hip").value) - parseInt(document.getElementById("neck").value)) + .22100 * this.log10(parseInt(document.getElementById("height").value))) - 450);
            bodyFat.innerHTML = bfFemale + " %";
            let fmFemale = Math.round(bfFemale / 100 * parseFloat(document.getElementById("weight").value));
            fatMass.innerHTML = fmFemale + " كجم";
            leanMass.innerHTML = parseFloat(document.getElementById("weight").value - fmFemale) + " كجم";
            if ((9 < parseInt(bfFemale)) && (parseInt(bfFemale) < 14)) {
                bfc.innerHTML = "دهون اساسية";
            } else if ((13 < parseInt(bfFemale)) && (parseInt(bfFemale) < 21)) {
                bfc.innerHTML = "رياضي محترف";
            } else if ((20 < parseInt(bfFemale)) && (parseInt(bfFemale) < 25)) {
                bfc.innerHTML = "فتنس";
            } else if ((24 < parseInt(bfFemale)) && (parseInt(bfFemale) < 32)) {
                bfc.innerHTML = "متوسط";
            } else if (31 < parseInt(bfFemale)) {
                bfc.innerHTML = "سمين";
            } else {
                bfc.innerHTML = "";
            }
        } else {
            let bfMale = Math.round(495 / (1.0324 - .19077 * this.log10(parseFloat(document.getElementById("abdomen").value) - parseFloat(document.getElementById("neck").value)) + .15456 * this.log10(parseFloat(document.getElementById("height").value))) - 450);
            bodyFat.innerHTML = bfMale + " %";
            let fmMale = Math.round(bfMale / 100 * parseFloat(document.getElementById("weight").value));
            fatMass.innerHTML = fmMale + " كجم";
            leanMass.innerHTML = parseFloat(document.getElementById("weight").value - fmMale) + " كجم";
            if ((1 < parseInt(bfMale)) && (parseInt(bfMale) < 6)) {
                bfc.innerHTML = "دهون اساسية";
            } else if ((5 < parseInt(bfMale)) && (parseInt(bfMale) < 14)) {
                bfc.innerHTML = "رياضي محترف";
            } else if ((13 < parseInt(bfMale)) && (parseInt(bfMale) < 18)) {
                bfc.innerHTML = "فتنس";
            } else if ((17 < parseInt(bfMale)) && (parseInt(bfMale) < 25)) {
                bfc.innerHTML = "متوسط";
            } else if (24 < parseInt(bfMale)) {
                bfc.innerHTML = "سمين";
            } else {
                bfc.innerHTML = "";
            }
        }
      },
      log10(val) {
          return Math.log(val) / Math.LN10;
      }
    }
  }
</script>
<style>
  table {
      background-color: #a39c94;
      font-size: 20px;
      border: 1px solid #000;
      border-bottom: none;
      border-spacing: 0px;
      margin: 10px auto;
  }

  tr {
      height: 44px;
  }

  td {
      padding: 10px;
      border-bottom: 1px solid #000;
  }

  @media only screen and (max-width: 767px) and (min-width: 0) {
    td{
      padding: 4px;
    }
  }

  span {
    margin-left: 25px;
  }

  .result {
    background-color: #8c837c;
  }

  input {
    margin-left: 5px;
    width:70px
  }

</style>
