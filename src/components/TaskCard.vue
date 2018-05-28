<template>
  <div class="card">
    <div class="card-content">
      {{ task.name }}
    </div>
    <footer class="card-footer">
      <div class="card-footer-item">
        {{ task.assignee }}
      </div>
      <div class="card-footer-item">
        {{ task.mandays }} 人日
      </div>
    </footer>
    <footer class="card-footer">
      <a class="card-footer-item" @click="decrementStatus(task)">◀︎</a>
      <a class="card-footer-item" @click="incrementStatus(task)">▶︎</a>
    </footer>
  </div>
</template>

<script>
export default {
  props: ['task'],
  methods: {
    incrementStatus: function (task) {
      if (task.status >= 1 && task.status <= 2) {
        task.status += 1
      }
    },
    decrementStatus: function (task) {
      if (task.status >= 2 && task.status <= 3) {
        task.status -= 1
      }
    }
  }
}
</script>
