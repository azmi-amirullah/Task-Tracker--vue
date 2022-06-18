<template>
  <AddTask v-show="showAddTask" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import Tasks from '../components/Tasks.vue'
import AddTask from '../components/AddTask.vue'

export default {
  name: 'Home',
  props: {
    showAddTask: Boolean
  },
  components: {
    Tasks,
    AddTask
  },
  data() {
    return { tasks: [] }
  },
  methods: {
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter(task => task.id !== id)
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map(task =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      )
    }
  },
  created() {
    this.tasks = [
      { id: 1, text: 'Meeting', day: 'June 1st at 12:30pm', reminder: true },
      { id: 2, text: 'Shopping', day: 'June 2st at 2:30pm', reminder: true },
      { id: 3, text: 'Car Wash', day: 'June 3st at 3:30pm', reminder: false }
    ]
  }
}
</script>
