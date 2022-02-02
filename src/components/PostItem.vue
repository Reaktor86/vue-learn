<template>
  <div class="post">
    <p class="title">{{ post.title }}</p>
    <p>{{ post.body }}</p>
    <div class="post__buttons">
      <my-button @click="removePost">Delete</my-button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    }
  },
  methods: {
    removePost() {
      this.$emit('remove', this.post);
    }
  }
}
</script>

<style scoped>
.post {
  margin: 10px;
  width: 700px;
  padding: 20px;
  border: 2px solid rgb(105, 214, 105);
}

.title {
  margin-bottom: 15px;
  font-size: 1.2em;
  font-weight: bold;
}

.post__buttons {
  margin-top: 10px;
  width: 100%;
  display: flex;
  gap: 5px;
  justify-content: flex-end;
}
</style>