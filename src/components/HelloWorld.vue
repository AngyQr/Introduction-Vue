<template>
  <div class="container">
    <h1>{{ msg }}</h1>
    <h2>TODO</h2>
    <div class="col-xs-12">
      <div class="d-flex">
        <input v-model="task" class="form-control mr-1" @keypress.enter="saveTask">
        <button class="btn btn-success" @click="saveTask">{{btnText}}</button>
      </div>
    </div>
    <div class="col-xs-12 mt-3">
      <h5 class="my-4 alert alert-dark d-flex justify-content-center"> Tasks List <span class="badge badge-success ml-2">{{tasksList.length}}</span></h5>
      <ul v-if="tasksList.length > 0" class="list-group">
        <template v-for="(task, index) in tasksList">
          <li :key="index" class="list-group-item">
            <div class="col-xs-12 d-flex justify-content-between">
              <h5> {{ task }}</h5>
              <div>
                <button class="btn btn-success btn-sm" @click="editTask(index)">
                  Edit
                </button>
                <button class="btn btn-danger btn-sm" @click="removeTask(index)">
                  Remove
                </button>
              </div>
            </div>
          </li>
        </template>
      </ul>
      <h5 v-else> No tasks </h5>
    </div>
    <div class="col-xs-12 mt-5 alert alert-success">
      <pre> {{$data}} </pre>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      indexTask: -1,
      task: '',
      tasksList: [],
      msg: 'Hello Vue.js',
      mode: true
    }
  },
  computed: {
    btnText () {
      return this.mode ? 'Agregar' : 'Guardar'
    }
  },
  methods: {
    saveTask () {
      if (this.mode) {
        this.tasksList.push(this.task)
      } else {
        this.tasksList[this.indexTask] = this.task
        this.mode = true
      }
      this.task = ''
    },
    removeTask (index) {
      this.tasksList.splice(index, 1)
    },
    editTask (index) {
      this.mode = false
      this.indexTask = index
      this.task = this.tasksList[index]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
a {
  color: #42b983;
}
</style>
