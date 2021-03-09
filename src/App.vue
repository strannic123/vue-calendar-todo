<template>
  <div class="parent">
    <div class="calendar">
      <AppCalendar @currentDay="onCurrentDay"/>
    </div>
    <div class="todo">
      <AppTodo :key="res"/>
      {{res}}
    </div>
  </div>



</template>

<script>
import AppCalendar from "@/components/AppCalendar";
import AppTodo from "@/components/AppTodo";

export default {
  name: 'App',
  data() {
    return {
      res: ''
    }
  },
  methods: {

    onCurrentDay(day, month, year){
      this.res = `${day} ${month} ${year}`




    },

  },
  components: {
    AppCalendar,
    AppTodo
  }
}
</script>

<style>
/*#app {*/
/*  font-family: Avenir, Helvetica, Arial, sans-serif;*/
/*  -webkit-font-smoothing: antialiased;*/
/*  -moz-osx-font-smoothing: grayscale;*/
/*  text-align: center;*/
/*  color: #2c3e50;*/
/*  margin-top: 60px;*/
/*}*/
.parent{
  display: flex;
  margin: 0 auto;
  flex-wrap: wrap;
}
.calendar{
  margin-right: 10px;
}
</style>
