<template>
  <q-page class="column bg-grey-3">
    <div class="row q-pa-sm bg-primary">
<q-input
          filled
          @keyup.enter="addTask"
          square
          bg-color="white"
          class="col"
          bottom-slots
          v-model="newTask"
          placeholder="Add Task"
          dense>        


    

        <template v-slot:append>
          <q-btn
            round
            dense
            flat
            @click="addTask"
            icon="add" />
        </template>
      </q-input>
    </div>
    <!-- <h5 class="q-mt-none">Todo</h5> -->
    <q-list separator bordered class="bg-white">
      <q-item
        v-for="(task, index) in tasks"
        @click="task.done = !task.done"
        :key="task.title"
        :class="{'done bg-blue-1' : task.done}"
        clickable
        v-ripple
      >
        <q-item-section avatar>
          <q-checkbox
            class="no-pointer-events"
            v-model="task.done"
            color="primary"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label> {{ task.title }} </q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn
          @click.stop = "deleteTask(index)"
            round
            color="red"
            icon="delete" />
        </q-item-section>
      </q-item>
    </q-list>
    <div v-if="!tasks.length" class="no-tasks absolute-center">
      <q-icon 
      name="check"
      size="100px"
      color="primary" />
      <div class="text-h5 text-primary text-center">
      No tasks
      </div>
    </div>
  </q-page>
</template>

<script>
// import { useQuasar } from "quasar";
import { defineComponent } from "vue";

export default defineComponent({
  // setup() {
  //   const $q = useQuasar()
  // },
  data() {
    return {
      newTask:'',
      tasks: [
        // {
        //   title: "Get Apples",
        //   done: false,
        // },
        // {
        //   title: "eat apples",
        //   done: false,
        // },
        // {
        //   title: "poop apples",
        //   done: false,
        // },
      ],
    };
  },
  methods: {
    deleteTask(index) {
       this.$q.dialog({
        title: 'Confirm',
        message: 'Really want to delete task?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        // console.log('>>>> OK')
        this.tasks.splice(index, 1);
        this.$q.notify('Task successfully deleted')
      })
    },
    addTask() {
      this.tasks.push({
        title:this.newTask,
        done:false
      });
      this.newTask="";

    }
  }
});
</script>

<style lang="scss">
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: #bbb;
    }
  }
  .no-tasks {
    opacity: 0.5;
  }
</style>
