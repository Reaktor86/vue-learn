<template>
  <div class="dialogue" v-if="show" @click="hideDialogue">
    <div class="dialogue__content" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "my-dialogue",
  props: {
    show: {
      type: Boolean,
      default: false,
    }
  },
  methods: {
    hideDialogue() {
      this.$emit('update:show', false);
    },
  }
}
</script>

<style scoped>
  .dialogue {
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    background: rgba(0,0,0,0.5);
    position: fixed;
    display: flex;
  }

  .dialogue__content {
    margin: auto;
    background: #fff;
    border-radius: 12px;
    min-height: 50px;
    min-width: 50px;
    padding: 20px;
  }
</style>