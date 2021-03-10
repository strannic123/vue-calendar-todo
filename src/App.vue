<template>
  <div class="parent">
    <div class="calendar">
      <AppCalendar @currentDay="onCurrentDay"/>
    </div>
    <div class="todo">
      <AppTodo :res="res"/>


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

body{
  background: #7bc0e352;
}

.parent{
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
.calendar{
  margin-right: 10px;
}
</style>
