<template>
  <div class="todo ">
    <v-text-field
      v-model="newTitleTask"
      @click:append="addTask"
      @keyup.enter="addTask"
      class="pa-3"
      outlined
      label="Add task"
      append-icon="mdi-plus"
      clearable
      hide-details
    ></v-text-field>

    <v-list class="pt-0" flat>
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'indigo lighten-5': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done }"
              >
                {{ task.title }}</v-list-item-title
              >
            </v-list-item-content>

            <v-list-item-action>
              <v-btn icon @click.stop="deleteTask(task.id)">
                <v-icon color="gray lighten-1">mdi-DotsVertical</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      newTitleTask: "",
      tasks: [],
    };
  },
  methods: {
    doneTask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },

    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },

    addTask() {
      if (this.newTitleTask) {
        let newTask = {
          id: Date.now(),
          title: this.newTitleTask,
          done: false,
        };

        this.tasks.push(newTask);
        this.newTitleTask = "";
      }
    },
  },
};
</script>
