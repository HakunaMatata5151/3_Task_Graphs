<script setup>
import { ref, shallowRef } from 'vue';
import { defineAsyncComponent } from 'vue'
import { VueDraggableNext } from 'vue-draggable-next'

const Column = shallowRef(defineAsyncComponent(() => {
  return import('@/components/Column_Graph.vue')
}))

const Donut = shallowRef(defineAsyncComponent(() => {
  return import('@/components/Donut_Graph.vue')
}))

const Line = shallowRef(defineAsyncComponent(() => {
  return import('@/components/Line_Graph.vue')
}))

const array = ref([
  {
    name: 'Column',
    id: 1,
    comp: Column,
    ready: true,
  },
  {
    name: 'Donut',
    id: 2,
    comp: Donut,
    ready: false,
  },
  {
    name: 'Line',
    id: 3,
    ready: false,
    comp: Line,
  },
]);

const draggable = VueDraggableNext;

function done(index) {
  if (index >= array.value.length - 1) {
    return;
  }
  array.value[index + 1].ready = true;
}

</script>

<template>
  <div class="main">
    <header>
      Welcome! Please Select the priority of graphs.
    </header>
    <div class="select-cover">
      <draggable class="select" :list="array">
        <div class="option" v-for="value in array" :key="value.id">
          <div class="ellipse">
            <img src="./assets/grip-vertical-solid.svg" />
          </div>
          <div> {{ value.name }}</div>
        </div>
      </draggable>
    </div>

    <div class="graphs">
      <div class="graph" :style="{ '--delay': `${index * .5}s` }" v-for="(value, index) in array" :key="value.id">
        <div class="name">
          {{ value.name }} :
        </div>
        <div v-if="value.ready">
          <component @done="done(index)" :is="value.comp" />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 40px;
}

.main header {
  font-size: 30px;
  font-weight: bolder;
}

.select-cover {
  margin-top: 22px;
  font-size: 18px;
}

.select {
  display: flex;
  gap: 22px;
}

.option {
  display: flex;
  cursor: pointer;
  color: #4e4e4e;
}

.ellipse {
  width: 15px;
  height: 19px;
}

.graphs {
  margin-top: 50px;
}

.graph {
  margin-top: 12px;
  animation: delay 1s ease-out forwards;
  opacity: 0;
  animation-delay: var(--delay);
}


@keyframes delay {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}
</style>
