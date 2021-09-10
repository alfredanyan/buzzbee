<template>
  <q-page class="q-pa-lg bg-grey-3">
    <h5 class="q-mt-none">Todo</h5>
    <q-list separator bordered class="bg-white">
      <q-item
        v-for="(task, index) in tasks"
        @click="task.done = !task.done"
        :key="task.title"
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
      tasks: [
        {
          title: "Get Apples",
          done: false,
        },
        {
          title: "eat apples",
          done: false,
        },
        {
          title: "poop apples",
          done: false,
        },
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
    }
  }
});
</script>
