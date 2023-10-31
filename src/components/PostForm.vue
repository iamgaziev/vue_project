<template>
  <div>
    <h1 class="text">Создание Поста</h1>
    <form @submit.prevent="createPost">
      <MyInput 
        type="text" 
        placeholder="title" 
        v-model="post.title" 
      />
      <MyInput 
        type="text" 
        placeholder="desc"
        v-model="post.body"
      /> 
      <MyButtons 
        class="btn"
        style="align-self: flex-end;"
        >
        add
      </MyButtons>
    </form>
  </div>
</template>

<script>
import MyButtons from './UI/MyButtons.vue';
import MyInput from './UI/MyInput.vue';


export default {

    data() {
        return {
            post: {
                title: "",
                body: ""
            }
        };
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            this.$emit("create", this.post);
            this.post = {
                title: "",
                body: ""
            };
        },
    },
    components: { MyButtons, MyButtons, MyInput }
};
</script>

<style scoped>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
form {
  display: flex;
  flex-direction: column;
}

.text {
  font-size: larger;
  font-weight: 800;
}

</style>
