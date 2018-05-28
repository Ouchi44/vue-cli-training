<template>
  <div class="container">
    <input type="text" v-model="newTask.name" />
    <select v-model="newTask.assignee">
      <option value="dog">🐶</option>
      <option value="cat">🐱</option>
      <option value="mouse">🐹</option>
    </select>
    <input type="number" v-model="newTask.mandays" />
    <button @click="addTask">追加</button>
    <hr />
    <div class="columns">
      <div class="column status-1">
        <div class="tags has-addons">
          <span class="tag">未対応</span>
          <span class="tag is-dark">{{ tasksOpen.length }}</span>
        </div>
        <transition-group name="fade">
          <task-card v-for="task in tasksOpen" :task="task" :key="task.name"></task-card>
        </transition-group>
      </div>
      <div class="column status-2">
        <div class="tags has-addons">
          <span class="tag">処理中</span>
          <span class="tag is-dark">{{ tasksDoing.length }}</span>
        </div>
        <transition-group name="fade">
          <task-card v-for="task in tasksDoing" :task="task" :key="task.name"></task-card>
        </transition-group>
      </div>
      <div class="column status-3">
        <div class="tags has-addons">
          <span class="tag">完了</span>
          <span class="tag is-dark">{{ tasksDone.length }}</span>
        </div>
        <transition-group name="fade">
          <task-card v-for="task in tasksDone" :task="task" :key="task.name"></task-card>
        </transition-group>
      </div>
    </div>
  </div>
</template>

<style>
.status-1 {
  background-color: #ed8077;
}
.status-2 {
  background-color: #4488c5;
}
.status-3 {
  background-color: #5eb5a6;
}
.card {
  margin-bottom: 5px;
}
.card-footer-item {
  padding-top: 0px;
  padding-bottom: 0px;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s
}
.fade-enter, .fade-leave-to {
  opacity: 0
}
</style>

<script>
import TaskCard from './TaskCard'
var filters = {
  open: function (tasks) {
    return tasks.filter(function (task) {
      return task.status === 1
    })
  },
  doing: function (tasks) {
    return tasks.filter(function (task) {
      return task.status === 2
    })
  },
  done: function (tasks) {
    return tasks.filter(function (task) {
      return task.status === 3
    })
  }
}

export default {
  components: {
    TaskCard
  },
  data () {
    return {
      tasks: [
        { name: 'task 1', status: 1, assignee: 'cat', mandays: 3 },
        { name: 'task 2', status: 1, assignee: 'dog', mandays: 2 },
        { name: 'task 3', status: 2, assignee: 'cat', mandays: 1 },
        { name: 'task 4', status: 3, assignee: 'mouse', mandays: 1 }
      ],
      newTask: {
        name: '', assignee: null, mandays: 0, status: 1
      }
    }
  },
  computed: {
    tasksOpen () {
      return filters.open(this.tasks)
    },
    tasksDoing () {
      return filters.doing(this.tasks)
    },
    tasksDone () {
      return filters.done(this.tasks)
    }
  },
  methods: {
    addTask () {
      this.tasks.push(this.newTask)
    }
  }
}
</script>
