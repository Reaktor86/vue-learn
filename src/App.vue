<template>
  <div class="app">
    <my-dialogue v-model:show="dialogueVisible">
      <PostForm @create="createPost"/>
    </my-dialogue>
    <button @click="addLike">Like</button>
    <button @click="addDislike">Dislike</button>
    <div>Кол-во лайков: <strong>{{ likes }}</strong></div>
    <div>Кол-во дизлайков: <strong>{{ dislikes }}</strong></div>
    <p v-if="isPostsLoading">Загружается</p>
    <div v-else>
      <my-button @click="showDialogue">Создать пост</my-button>
      <my-select
        v-model="selectedSort"
        :options="sortOptions"
      />
      <PostList 
        :posts="posts"
        @remove="removePost"
      />
    </div>
    
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from 'axios';

export default {
  components: {
    PostForm, PostList
  },
  data() {
    return {
      likes: 0,
      dislikes: 0,
      posts: [],
      dialogueVisible: false,
      isPostsLoading: true,
      selectedSort: '',
      sortOptions: [
        {value: 'title', name: 'по названию'},
        {value: 'body', name: 'по содержимому'},
      ],
    }
  },

  methods: {
    addLike() {
      this.likes += 1;
    },

    addDislike() {
      this.dislikes += 1;
    },

    createPost(post) {
      this.posts.push(post);
      this.dialogueVisible = false;
    },

    removePost(post) {
      console.log('App, post = ', post);
      this.posts = this.posts.filter(item => item.id !== post.id);
    },

    showDialogue() {
      this.dialogueVisible = true;
    },

    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        setTimeout( async () => {
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _limit: 10
            }
        });
        this.posts = response.data;
        this.isPostsLoading = false;
        }, 500);
        
      } catch (e) {
        throw Error(e.message);
      }
    },
  },

  mounted() {
    this.fetchPosts();
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

</style>