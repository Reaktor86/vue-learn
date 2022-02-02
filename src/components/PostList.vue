<template>
  <div v-if="posts.length > 0">
    <h3>Список статей</h3>
    <PostItem 
      v-for="post in posts" 
      :key="post.id" 
      :post="post"
      @remove="removePost"
    />
  </div>
  <h4 v-else>Пусто</h4>
</template>

<script>
import PostItem from "@/components/PostItem";
export default {
  components: {
    PostItem,
  },
  props: {
    posts: {
      type: Array,
      required: true,
    }
  },
  methods: {
    removePost(post) {
      console.log('PostList, post = ', post);
      this.$emit('remove', post);
    }
  }
}
</script>

<style scoped>



</style>