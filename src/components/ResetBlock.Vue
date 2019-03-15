<template>
  <div class="card-box">
    <b-button class="button effect pulse" @click="resetPage">RESET</b-button>
  </div>
</template>

<script>
export default {
  methods: {
    resetPage() {
      this.$emit("refreshPage");
    }
  }
};
</script>

<style>

</style>
