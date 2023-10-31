<template>
  <div class="post">
    <div>
      <div><strong>Название:</strong> {{ elem.title }}</div>
      <div><strong>Описание:</strong> {{ elem.body }}</div>
    </div>
    <div class="post__btn">
      <My-Buttons 
      @click="$emit('remove', post)"
      >
        Удалить
      </My-Buttons>
    </div>
  </div>
</template>

<script>
import MyButtons from './UI/MyButtons.vue';

export default {

    props: {
        elem: {
            type: Object,
            required: true,
        },
    },
    components: {  MyButtons }
};
</script>

<style scoped>
.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
