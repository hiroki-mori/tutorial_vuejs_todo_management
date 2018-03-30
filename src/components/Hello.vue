<template>
  <div>
    {{ msg }}
    <form>
      <button @click="addTask()">ADD TASK</button>
      <button @click="removeTask()">DELETE FINISHED TASKS</button>
      <p>input:<input type='text' v-model="newTask"></p>
      <p>task: {{newTask}}</p>
    </form>
    <div class="task-list">
      <label class="task-list__item" v-for="task in tasks" v-bind:class="{ 'task-list__item--checked' : task.done }">
        <input type="checkbox" v-model="task.done">
        <input type="checkbox" v-model="task.editing">
        <input v-if="task.editing" v-model="task.text" @keyup.enter="task.editing = !task.editing">
        <span v-else>{{ task.text }}</span>

      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data: function() {
    return {
      msg: 'Welcome to Your Vue.js App',
      tasks: [
        {text : 'vue-router', done: false, editing:false},
        {text : 'vuex', done: false, editing:false},
        {text : 'vue-loader', done: false, editing:false},
        {text : 'awesome-vue', done: true, editing:false},
      ],
      newTask: ""
    }
  },
  methods:{
    addTask: function(event){
      let text = this.newTask && this.newTask.trim()
      if(!text){
        return
      }
      this.tasks.push({
        text:text,
        done:false
      })
      this.newTask = ''
    },
    removeTask: function(event){
      for (let i = this.tasks.length - 1;i>=0;i--){
        if(this.tasks[i].done) this.tasks.splice(i,1)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@mixin flex-vender(){
  display:flex;
  display:-webkit-flex;
  display:-moz-flex;
  display:-ms-flex;
  display:-o-flex;
}
.task-list{
  @include flex-vender;
  flex-direction:column;
  align-items: center;
  &__item{
    width:270px;
    text-align: left;
    $element: #{&};
    &--checked{
      @extend #{$element};
      color: #85a6c6;
    }
  }
}
</style>
