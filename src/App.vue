<template>
  <div id="app">
    <h1>Task List</h1>

      <div class="box">
        <input class="input" type="text" placeholder="Title" v-model="newTaskTtitle">
        <input class="input" type="text" placeholder="Content　Shift＋Enterで登録" v-model="newTaskComment" v-on:keyup.shift.enter="addTodo">
      </div>

    <draggable :options="{ group: 'tasks' }" element="ul" v-for="(list,taskIndex) in tasks" v-bind:class="['task__' + taskIndex]">
      <li class="card" v-for="(item,listIndex) in list" :key="item.status">
        <div class="card-content text">{{ item.name }}</div>
        <div v-if="!isComment" v-on:dblclick="isComment = true">
          <div class="card-footer-item">{{ item.comment }}</div>
        </div>
        <div v-else>
          <input type="text" class="input is-rounded" v-model="item.comment" v-on:blur="isComment=false">
        </div>
          <span class="delele" v-on:click="doDelete(taskIndex, listIndex)">削除</span>
      </li>
    </draggable>
  </div>
</template>

<script>
import draggable from 'vuedraggable';

export default {
  name: 'App',
  components: {
    draggable,
  },
  data() {
    return {
      tasks: [
      [{ name: '初代', status: 1, comment: "ピカチュウ" },{ name: '初代', status: 1, comment: "カイリュウ" } ],
      [{ name: '金銀', status: 2, comment: "ヤドキング" },{ name: '金銀', status: 2, comment: "ランターン" } ],
      [{ name: '第三世代', status: 3, comment: "キモリ" },{ name: '第三世代', status: 3, comment: "アチャモ" } ],
      ],
      isComment: false,
      newTaskTtitle: '',
      newTaskComment: '',
    }
  },
  methods: {
    addTodo: function(){
      this.tasks[0].push({name: this.newTaskTtitle, comment: this.newTaskComment});
      this.newTaskTtitle = "",
      this.newTaskComment = ""
    },
    doDelete: function(taskIndex,listIndex){
      this.tasks[taskIndex].splice(listIndex,1);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 2rem;
}

h1 {
  margin-bottom: 10px;
}

ul {
  display: inline-block;
  vertical-align: top;
  width: 25%;
  padding: 10px;
}

.box {
  width: 70%;
  margin: 0 auto;
}

.card{
  padding:7px;
  margin: 0 auto;
}

.task__0{
  background-color: #ed8077;
}

.task__1{
  background-color: #edcd77;
}

.task__2{
  background-color: #5eb5a6;
}

.input{
  margin-bottom: 10px;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave {
  opacity: 0
}

</style>
