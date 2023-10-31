<template>
  <div v-if="posts.length > 0">
    <h3>Список пользователья</h3>
    <PostItem 
    class="post" v-for="elem in posts" 
    :elem="elem" 
    :key="elem.id"
    @remove="$emit('remove', elem)" 
    />
  </div>
  <h2 v-else style="color: red; margin-top: 25px;">
    Список пользователей пуст
  </h2>
</template>

<script>
import PostItem from "./PostItem.vue";

export default {
  components: {
    PostItem,
  },
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped></style>
