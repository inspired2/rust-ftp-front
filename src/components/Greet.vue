<script setup>
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/tauri";

const state = ref([]);
setInterval(async () => {
  await updateState()
}, 1000);
function sortHelper(state) {

}
function updateHelper(oldState, newState) {
  newState.forEach( ent => {
    if (!oldState.contains(ent)) {
      oldState.push(ent);
      sortState(oldState);
    }
  })
}
async function updateState() {
  let newState = await invoke("get");
  updateHelper(state, newState);
}
</script>

<template>
  <div class="card">
    <!-- <input id="greet-input" v-model="name" placeholder="Enter a name..." />
    <button type="button" @click="updateState()">Greet</button> -->
  </div>

  <p :key = "ent" v-for="ent in state">{{ ent }}</p>
</template>
