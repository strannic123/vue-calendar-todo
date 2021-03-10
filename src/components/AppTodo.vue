<template>
  <div class="container">
    <div class="title">
      <h1>Список дел</h1>

      <h2>{{ saveDate }}</h2>

    </div>

    <div class="addTask">
      <input
          class="input_task"
          v-model="input"
          @keydown.enter="addItem"

      >
      <button @click="addItem">Добавить</button>
    </div>

    <div class="tasks_list">
      <ul>
        <template v-for="(elem, index) of list">
          <li
              v-if="elem.date == res"
              class="task"
              :key="index"
          >
      <span><span>
        <input
            @click="changeChecked(index)"
            class="checkbox"
            type="checkbox">

      </span>


        <input
            v-model="inputChange"
            v-if="list[index].changeItem"
            @keydown.enter="addChangeElem(index)"
            type="text"/>

      <span
          v-else
          @dblclick="editItem(index)"
          :class="{done: list[index].checked}">{{ elem.title }}</span>

      </span>
            <button @click="removeEl(index)" class="delete">X</button>
          </li>
        </template>

      </ul>
    </div>
    <p v-if="saveDate == '' "> <b>Выберите дату-добавьте задачу</b></p>


  </div>
</template>

<script>
export default {
  name: "App",
  props: ['res'],

  data() {
    return {
      input: '',
      inputChange: '',
      list: [],
      idElem: '',
      dateNow: new Date().toLocaleDateString()
    }
  },
  methods: {
    addItem() {
      let el = {
        checked: false,
        title: this.input,
        changeItem: false,
        id: Math.random(),
        date: this.idElem
      }
      this.list.push(el)
      this.input = ''
      console.log(this.dateNow)
    },

    changeChecked(index) {
      this.list[index].checked = !this.list[index].checked
    },

    removeEl(index) {
      this.list.splice(index, 1)
    },

    editItem(index) {
      this.list[index].changeItem = true
      this.inputChange = this.list[index].title
    },

    addChangeElem(index) {
      this.list[index].title = this.inputChange
      this.list[index].changeItem = false
    },
  },

  computed: {
    saveDate() {
      return this.idElem = this.res
    }
  }
}
</script>


<style scoped>
body {
  font-family: Inter, Roboto, Oxygen, Fira Sans, Helvetica Neue, sans-serif;
  background: #6593aa;
  color: #fff;
}

.task {
  display: flex;
  justify-content: space-between;
  list-style-type: none;
  cursor: pointer;
  border: 1px solid #00ffb1;
  border-radius: 10px;
  background: #fff;
  color: black;
  padding: 10px;
  margin-bottom: 5px;
}

.input_task {
  width: 300px;
  font-size: 13px;
  padding: 6px 0 4px 10px;
  border: 1px solid #cecece;
  background: #F6F6f6;
  border-radius: 8px;
}

button {
  border: 1px solid limegreen;
  border-radius: 40px;
  width: 150px;
  height: 30px;
  margin-left: 10px;
}

button:active {
  border: 3px solid lightseagreen;
}

button:active, button:focus, input:active, input:focus {
  outline: none;
}

button::-moz-focus-inner {
  border: 0;
}

.delete {
  border: 1px solid red;
  width: 25px;
  height: 25px;
  background: #ed9d9d;
}

.delete:active {
  border: 3px solid crimson;
}

.done {
  color: #7d7e82;
  text-decoration: line-through;
}

.dNone {
  display: none;
}

.container {
  margin: 0 auto;
  max-width: 650px;
  display: flex;
  flex-direction: column;
}

.container h1 {
  margin: 15px auto;
}

.container .title {
  margin: 0 auto;
}
.container p{
  text-align: center;
}

.addTask {
  display: flex;
  margin: 0 auto;
  width: 100%;
  border-radius: 3px;
}

.tasks_list ul {
  padding-left: 0;
}

.checkbox {
  margin-right: 10px;
}
</style>
