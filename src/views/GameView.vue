<script setup>
import {computed, reactive, ref} from "vue";

const state = reactive({ xsize: 0, ysize: 0 })

const itemRefs = ref([])

const hover = (index) => {
  const x = index.split(',')[0]
  const y = index.split(',')[1]
  let currentColor = itemRefs.value[x].children[y].style.background
  itemRefs.value[x].children[y].style.background = currentColor === 'white' ? "blue" : "white"
}

const redraw = computed(() => {
  return state.xsize + state.ysize
})

</script>

<template>
  <div style="width: 1200px; height: 100vh; padding: 2rem">
    <div>
      <v-text-field v-model="state.xsize" label="Xsize" required type="number"></v-text-field>
      <v-text-field v-model="state.ysize" label="Ysize" required type="number"></v-text-field>
    </div>
    <div :key="redraw" style="margin: 2rem 0; background: black; display: grid; overflow-x: scroll">
      <div style="display: flex; flex-direction: column">
        <div ref="itemRefs" v-for="(_, y) in +state.ysize" :key="y" style="display: flex" >
            <div
              v-for="(_, x) in +state.xsize"
              :key="x"
              style="width: 36px; height: 36px; margin: 1rem; display: flex; background: white;"
              @mouseover="hover(y + ',' + x)"
            >
            </div>
        </div>
      </div>
    </div>
  </div>
</template>
