<template>
  <div class="flex gap-[40px] w-full p-20 mx-auto justify-center">
 
    <div class="w-full xl:w-1/2">
      <draggable
        v-model="questions[currentQuestion].items"
        tag="ul"
        :animation="300"
      >
        <template #item="{ element: item }">
          <li class="item">
            {{ item.name }}
          </li>
        </template>
      </draggable>
      <button class="w-full mt-4 p-2 bg-blue-400">
        Следующий вопрос
      </button>
    </div>
  </div>
</template>

<script setup>
import draggable from 'vuedraggable';
import { ref } from 'vue';
const questions = ref([
  {
    items: [
      { id: '1', name: 'Ответ 1' },
      { id: '2', name: 'Ответ 2' },
      { id: '3', name: 'Ответ 3' },
      { id: '4', name: 'Ответ 4' },
    ],
    correctOrder: ['1', '2', '3', '4'],
  },
  {
    items: [
      { id: '5', name: 'Ответ 5' },
      { id: '6', name: 'Ответ 6' },
      { id: '7', name: 'Ответ 7' },
      { id: '8', name: 'Ответ 8' },
    ],
    correctOrder: ['5', '6', '7', '8'],
  },
  {
    items: [
      { id: '9', name: 'Ответ 9' },
      { id: '10', name: 'Ответ 10' },
      { id: '11', name: 'Ответ 11' },
      { id: '12', name: 'Ответ 12' },
    ],
    correctOrder: ['9', '10', '11', '12'],
  },
]);

const currentQuestion = ref(0);

</script>


<style>
.item {
  height: 40px;
  width: 200px;
  background-color: aqua;
  color: black;
  padding: 10px;
  margin-bottom: 20px;
}
</style>