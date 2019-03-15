<template>
  <div class="card-box">
    <b-card class="card-content">
      <span class="group-box">
        <b-card-text class="text">
          DATA
          <input
            type="text"
            class="input-line"
            placeholder="Type Here.."
            v-model="dataName"
          />
        </b-card-text>
      </span>
      <b-button class="button effect pulse" @click="addNewBlock"
        >+ ADD NEW BLOCK</b-button
      >
    </b-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dataName: ""
    };
  },
  methods: {
    addNewBlock() {
      this.$emit("accept", this.dataName);
    }
  }
};
</script>

<style></style>
