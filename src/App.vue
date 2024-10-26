<template>
  <div>
    <div>
      <Container
        group-name="items"
        :get-child-payload="(index) => questions[currentQuestion].items[index]"
        @drop="onDrop"
      >
        <Draggable
          v-for="item in questions[currentQuestion].items"
          :key="item.id"
        >
          <div class="item">
            {{ item.data }}
          </div>
        </Draggable>
      </Container>

    </div>
  </div>
</template>

<script>
import { Container, Draggable } from 'vue-dndrop';

export default {
  name: 'DnD',
  components: {
    Container,
    Draggable,
  },
  data() {
    return {
      currentQuestion: 0,
      errorMessage: '',
      questions: [
        {
          items: [
            { id: '1', data: 'Ответ 1-1' },
            { id: '2', data: 'Ответ 1-2' },
            { id: '3', data: 'Ответ 1-3' },
            { id: '4', data: 'Ответ 1-4' },
          ],
          correctOrder: ['1', '2', '3', '4'],
        },
      ],
    };
  },
  methods: {
    onDrop(dropResult) {
      const updatedItems = this.handleDrag(
        this.questions[this.currentQuestion].items,
        dropResult,
      );
      this.questions[this.currentQuestion].items = updatedItems;
    },
    handleDrag(items, dropResult) {
      const { removedIndex, addedIndex, payload } = dropResult;
      if (removedIndex === null && addedIndex === null) return items;

      const result = [...items];
      let itemToAdd = payload;

      if (removedIndex !== null) {
        itemToAdd = result.splice(removedIndex, 1)[0];
      }

      if (addedIndex !== null) {
        result.splice(addedIndex, 0, itemToAdd);
      }
      return result;
    },
  },
};
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