<script setup>
import {reactive} from "vue";

const state = reactive({
  xsize: '',
  ysize: '',
  start: false,
  backgrounds: {
    x: [],
    y: []
  }
})

const handleStart = () => {
  if (state.xsize && state.ysize) {
    state.start = true
  }
}

const hover = (z, index) => {
  const currentBg = state.backgrounds[z][index]
  state.backgrounds[z][index] = (currentBg === "blue") ? "white" : "blue"
}

</script>

<template>
  <div style="width: 1200px; height: 100vh; padding: 2rem">
    <div>
      <v-text-field
        v-model="state.xsize"
        label="Xsize"
        required
      ></v-text-field>
      <v-text-field
        v-model="state.ysize"
        label="Ysize"
        required
      ></v-text-field>
      <v-btn
        v-if="!state.start"
        class="me-4"
        @click="handleStart"
      >
        start
      </v-btn>
    </div>
    <div v-if="state.start" style="margin: 2rem 0; background: black">
      <div style="display: flex;">
        <div
          v-for="(item, index) in +state.xsize"
          :key="index"
          style="width: 36px; height: 36px; margin: 1rem; display: flex"
          @mouseover="hover('x', index)"
          :class="$style[(state.backgrounds.x.length > 0 && state.backgrounds.x[index]) ? state.backgrounds.x[index] : 'white']"
        >
        </div>
      </div>
      <div style="display: flex; flex-direction: column">
        <div
          v-for="(item, index) in +state.ysize-1"
          :key="index"
          style="width: 36px; height: 36px; margin: 1rem; display: flex"
          @mouseover="hover('y', index)"
          :class="$style[(state.backgrounds.y.length > 0 && state.backgrounds.y[index]) ? state.backgrounds.y[index] : 'white']"
        >
        </div>
      </div>
    </div>
  </div>
</template>

<style module>
.white {
  background: white;
}
.blue {
  background: blue;
}
/*@media (min-width: 1024px) {*/
/*  .about {*/
/*    min-height: 100vh;*/
/*    display: flex;*/
/*    align-items: center;*/
/*  }*/
/*}*/
</style>
