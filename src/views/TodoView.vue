<template>
  <div class="home">
    <v-text-field
    v-model="newTaskTitle"
    @click:append="addTask"
    @keyup.enter="addTask"
    class="pa-3"
      outlined
      label="Add Task"
      append-icon="mdi-plus"
      hide-details
      clearbale
      ></v-text-field>
    <v-list class="pt-0" flat>
      <template v-for="(task, index) in tasks">
        <v-list-item :key="task.id" @click="doneTask(task.id)" :class="{ 'blue lighten-5': task.done }">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title :class="{ 'text-decoration-line-through': task.done }">{{ task.title }}</v-list-item-title>
            </v-list-item-content>
            
            <v-list-item-action>
              <v-btn 
              @click.stop="deleteTask(task.id)"
              icon>
                <v-icon color="primary lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <!-- Divider after each list item except for the last one -->
        <v-divider v-if="index !== tasks.length - 1"></v-divider>
      </template>
    </v-list>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      newTaskTitle:'',
      tasks: [
        { id: 1, title: 'Wake up', done: false },
        { id: 2, title: 'Have tea', done: false },
        { id: 3, title: 'Go for a walk', done: false }
      ]
    };
  },
  methods: {
    addTask(){
      let newTask = {
        id:Date.now(),
        title:this.newTaskTitle,
        done:false
      }
      this.tasks.push(newTask)
      this.newTaskTitle=''
    },
    doneTask(id) {
      let task = this.tasks.find(task => task.id === id);
      task.done = !task.done;
    },
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id != id)
    }
  }
};
</script>
