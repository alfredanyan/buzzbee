<template>
  <q-page class="q-pa-lg bg-grey-3">
    <h5 class="q-mt-none">Todo</h5>
    <q-list separator bordered class="bg-white">
      <q-item
        v-for="task in tasks"
        @click="task.done = !task.done"
        :key="task.title"
        clickable
        v-ripple
      >
        <q-item-section avatar>
<q-checkbox
            class="no-pointer-events"
            v-model="task.done"
            color="primary" />

        </q-item-section>
        <q-item-section>
          <q-item-label> {{ task.title }} </q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
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
});
</script>
