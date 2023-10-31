<template>
  <div class="app">
    <MyInput v-model="searchQuery" @input="searchFunc" placeholder="Поиск..." />
    <h3 class="text">Страница с постами</h3>
    <MyButtons @click="showDialog"> Создать пользователья </MyButtons>
    <Modal :show="dialogVisible">
      <PostForm @create="createPost" />
    </Modal>
    <PostList
      :posts="newPost.length !== 0 ? newPost : posts"
      @remove="removePost"
      v-if="!isPostsLoading"
    />
    <div class="loading" v-else>Идёт загрузка...</div>
  </div>
</template>

<script>
import axios from "axios";
import PostForm from "./components/PostForm.vue";
import PostList from "./components/PostList.vue";
import Modal from "./components/UI/Modal.vue";
import MyButtons from "./components/UI/MyButtons.vue";
import MyInput from "./components/UI/MyInput.vue";

export default {
  components: {
    PostList,
    PostForm,
    Modal,
    MyButtons,
    MyInput,
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: false,
      searchQuery: "",
      newPost: [],
    };
  },
  methods: {
    createPost(elem) {
      this.posts.unshift(elem);
      this.dialogVisible = false;
    },
    
    removePost(post) {
      this.posts = this.posts.filter(elem => elem.id !== post.id);
    },
    showDialog() {
      this.dialogVisible = true;
    },
    searchFunc() {
      this.newPost = this.posts.filter((elem) =>elem.title.toLowerCase().includes(this.searchQuery.toLowerCase()));
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        setTimeout(async () => {
          let { data } = await axios.get(
            "https://jsonplaceholder.typicode.com/posts",
            {
              params: {
                _limit: 10
              },
            }
          );
          this.posts = data;
          this.isPostsLoading = false;
        }, 1000);
      } catch (error) {
        alert("Ошибка!");
      }
    },
  },
  mounted() {
    this.fetchPosts();
  },
};
</script>

<style scoped>
* {
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
}
.app {
  padding: 20px;
}
.text {
  margin-top: 2%;
}
.loading {
  text-align: center;
  font-size: xx-large;
  font-weight: 800;
  margin-top: 5%;
}
</style>
