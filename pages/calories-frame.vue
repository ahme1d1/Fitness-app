<template>
  <div class="container pt-5">
    <table>
      <tr>
        <td>
          <span>الجنس</span>
        </td>
        <td>
          <input type="radio" id="female" checked="checked" name="Gender">امرأة
          <input type="radio" id="male" name="Gender">رجل
        </td>
      </tr>
      <tr>
        <td>
          <span>السن</span>
        </td>
        <td>
          <input type="text" id="age" value="">سنة
        </td>
      </tr>
      <tr>
        <td>
          <span>الوزن</span>
        </td>
        <td>
          <input type="text" id="weight" value="">كجم
        </td>
      </tr>
      <tr>
        <td>
          <span>الطول</span>
        </td>
        <td>
          <input type="text" id="height" value="">سم
        </td>
      </tr>
      <tr>
        <td>
          <span>المعادلة</span>
        </td>
        <td>
          <input type="radio" id="m" v-on:click="del();" checked="checked" name="Formula">ملفين سانت جوير
          <br><input type="radio" id="h" v-on:click="del();" name="Formula">هاريس بندكت
          <br><input type="radio" id="k" v-on:click="add();" name="Formula">كاتش ماكردل
        </td>
      </tr>
      <tr id="fat" style="visibility:hidden;display:none;">
        <td>
          <span>الدهون</span>
        </td>
        <td>
          <input type="text" id="bf" value="" style="width:40px">%
        </td>
      </tr>
      <tr>
        <td>
          <span>مستوى النشاط</span>
        </td>
        <td>
          <select id="op" style="font-size:22px;width:80%;">
            <option value="1">معدل الايض الاساسي</option>
            <option value="1.2">لا تمرين</option>
            <option value="1.375">3 مرات اسبوعيا</option>
            <option value="1.42">4 مرات اسبوعيا</option>
            <option value="1.46">5 مرات اسبوعيا</option>
            <option value="1.505">6 مرات اسبوعيا</option>
            <option value="1.55">5 مرات اسبوعيا بشدة عالية</option>
            <option value="1.64">كل يوم</option>
            <option value="1.725">كل يوم بشدة عالية او مرتين يوميا</option>
            <option value="1.9"> كل يوم + وظيفة شاقة</option>
          </select>
          <button style="background-color: #FE2E2E;cursor:pointer;font-size:25px;color:white;border:none;margin-top:5px;" type="button" v-on:click="check()">احسب الاحتياج</button>
        </td>
      </tr>
      <tr class="result">
        <td style="text-align: center;font-size:21px">معدل الأيض الاساسي:</td>
        <td>
          <span id="bmr">
            0
          </span>
          سعر حراري /يوم
        </td>
      </tr>
      <tr class="result">
        <td style="text-align: center;font-size:21px;">الاحتياجات اليومية من السعرات:</td>
        <td>
          <span id="tdee">
            0
          </span>
          سعر حراري /يوم
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
  export default {
    methods: {
      del(){
          document.getElementById("fat").setAttribute("style","visibility: hidden");
      },
      add(){
        document.getElementById("fat").setAttribute("style","visibility: visible");
      },
      check(){
          let age=document.getElementById("age").value;
          let weight=document.getElementById("weight").value;
          let height=document.getElementById("height").value;
          let op=document.getElementById("op").value;
          let bf=document.getElementById("bf").value;
          let bmr=document.getElementById("bmr");
          bmr.innerHTML="";
          let tde=document.getElementById("tdee");
          tde.innerHTML="";
          if(document.getElementById("female").checked)
          {
              if(document.getElementById("m").checked)
              {
                  bmr.innerHTML=Math.round(10*weight+6.25*height-5*age-161);
              }
              else if(document.getElementById("h").checked)
              {
                    bmr.innerHTML=Math.round(655.1+(9.563*weight)+(1.85*height)-(4.676*age));
              }
              else
              {
                  bmr.innerHTML=Math.round(21.6*(weight-(bf/100*parseFloat(weight)))+370);
              }
              tde.innerHTML=Math.round(parseFloat(document.getElementById("bmr").innerHTML)*parseFloat(op));
          }
          else
          {
              if(document.getElementById("m").checked)
              {

                  bmr.innerHTML=Math.round(10*weight+6.25*height-5*age+5);
              }
              else if(document.getElementById("h").checked)
              {
                  bmr.innerHTML=Math.round(66.5+(13.75*weight)+(5.003*height)-(6.775*age));
              }
              else
              {
                  bmr.innerHTML=Math.round(21.6*(weight-(bf/100*parseFloat(weight)))+370);
              }
              tde.innerHTML=Math.round(parseFloat(document.getElementById("bmr").innerHTML)*parseFloat(op));
          }
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
