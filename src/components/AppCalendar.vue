<template>
  <div id="app">
    <table class="table">
      <thead>
      <tr>
        <td>
          <button v-on:click="decrease">&lt;</button>
        </td>
        <td colspan="5" > {{monthes[month]}} {{year}} </td>
        <td>
          <button v-on:click="increase">></button>
        </td>
      </tr>
      <tr >
        <td v-for="d in day">{{d}}</td>
      </tr>
      </thead>
      <tbody>
      <tr v-for="week in calendar()">
        <td
            v-for="(day, index) in week" :style="{'color': day.weekend, 'background-color': day.current}"
            @click="$emit('currentDay', day.index, monthes[month], year)"
        > {{ day.index }} </td>
      </tr>
      </tbody>
    </table>
<!--    <div class="format-week">-->
<!--      <h4>Format week</h4>-->
<!--      <div>-->
<!--        <input type="radio" value="1" v-model="dFirstMonth" id="customRadio1" name="customRadio" class="custom-control-input">-->
<!--        <label for="customRadio1">Monday</label>-->
<!--      </div>-->
<!--      <div>-->
<!--        <input type="radio" value="0" v-model="dFirstMonth" id="customRadio2" name="customRadio" class="custom-control-input">-->
<!--        <label for="customRadio2">Sunday</label>-->
<!--      </div>-->
<!--    </div>-->

  </div>
</template>

<script>
export default {
  emits: ['currentDay'],
  name: "AppCalendar",
    data() {
      return {
        month: new Date().getMonth(),
        year: new Date().getFullYear(),
        dFirstMonth: '1',
        day:["Пн", "Вт","Ср","Чт","Пт","Сб", "Вс"],
        monthes: ["Январь","Февраль","Март","Апрель","Май","Июнь","Июль","Август","Сентябрь","Октябрь","Ноябрь","Декабрь"],
        date: new Date(),
      }
    },

    methods:{
      calendar: function(){
        let days = [];
        let week = 0;
        days[week] = [];
        let dlast = new Date(this.year, this.month + 1, 0).getDate();
        for (let i = 1; i <= dlast; i++) {
          if (new Date(this.year, this.month, i).getDay() != this.dFirstMonth) {
           let a = {index:i};
            days[week].push(a);
            if (i == new Date().getDate() && this.year == new Date().getFullYear() && this.month == new Date().getMonth()) { a.current = '#747ae6'};
            if (new Date(this.year, this.month, i).getDay() == 6 || new Date(this.year, this.month, i).getDay() == 0) { a.weekend = '#ff0000'};
          }
          else {
            week++;

            days[week] = [];
           let a = {index:i};
            days[week].push(a);
            if ((i == new Date().getDate()) && (this.year == new Date().getFullYear()) && (this.month == new Date().getMonth())) { a.current = '#747ae6'};
            if (new Date(this.year, this.month, i).getDay() == 6 || new Date(this.year, this.month, i).getDay() == 0) { a.weekend = '#ff0000'};
          }
        }

        if (days[0].length > 0) {
          for (let i = days[0].length; i < 7; i++) {
            days[0].unshift('');

          }
        }
        // this.dayChange;
        // console.log(days);
        return days;
      },
      decrease: function(){
        this.month--;
        if (this.month < 0) {
          this.month = 12;
          this.month--;
          this.year--;
        }

      },
      increase: function(){

        this.month++;
        if (this.month > 11) {
          this.month = -1;
          this.month++;
          this.year++;
        }
      },

    },
    computed: {
      // dayChange: function(){
      //   if(this.dFirstMonth == 0){
      //     this.day = [ "Вс", "Пн", "Вт","Ср","Чт","Пт","Сб",]
      //   }else{
      //     this.day = ["Пн", "Вт","Ср","Чт","Пт","Сб", "Вс"]
      //   }
      // },
    },


}
</script>

<style scoped>

.table {
  border-collapse: collapse;
  float: left;
  /*width: 180px;*/
  /*table-layout: fixed;*/
}
.format-week {
  float:right;
}
.table td {
  text-align:center;
  width: 50px;
  height: 50px;
  font-size: 20px;
  cursor: pointer;

}
.table thead tr:last-child {
  background-color: #dedada;
}


</style>
