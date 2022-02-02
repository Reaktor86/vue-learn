<template>
  <h3>Заполните форму</h3>
  <my-input placeholder="post name" v-model.trim="post.title"/>
  <my-input placeholder="post text" v-model.trim="post.body"/>
  <my-button @click="createPost">Create</my-button>
</template>

<script>
import MyInput from './UI/MyInput.vue';
export default {
  components: { MyInput },
  data() {
    return {
      post: {
        id: 0,
        title: '',
        body: '',
      }
    }
  },

  methods: {
    createPost() {
        this.post.id = Date.now();
        this.$emit('create', this.post);
        this.post = {
          id: 0,
          title: '',
          body: '',
        }
      }
  },
}
</script>

<style scoped>

</style>