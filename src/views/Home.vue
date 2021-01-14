<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/> -->
    <counter v-model="initCounter" />
    <div>
      <input type="number" v-model.number="initCounter" id="" />
    </div>
    {{ notes }}
    <note-to-do v-model:notes="notes"> </note-to-do>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import counter from "@/components/counter.vue";
import NoteToDo from "@/components/noteToDo.vue";

@Options({
  components: {
    counter,
    NoteToDo,
  },
})
export default class Home extends Vue {
  initCounter = 5;
  notes = [];
}
</script>
