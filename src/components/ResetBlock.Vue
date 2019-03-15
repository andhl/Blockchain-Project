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

<style scoped>
.pulse {
  animation: pulse 1s infinite;
}

@keyframes pulse {
  0% {
    box-shadow: 0 0 0 0px rgba(167, 32, 208, 0.5);
  }
  100% {
    box-shadow: 0 0 0 10px rgba(252, 249, 255, 0);
  }
}

@keyframes pulse-2 {
  0% {
    box-shadow: 0 0 0 0px rgba(167, 32, 208, 0.5);
  }
  100% {
    box-shadow: 0 0 0 100px rgba(0, 0, 0, 0);
  }
}

.card-box {
  width: 10%;
  margin-left: auto;
  padding-bottom: 5%;
}

.button {
  border-color: transparent;
  color: transparent;
  margin: 5px;
  padding: 15px;
  text-align: center;
  color: white;
  border-radius: 50px;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 0.75rem;
}

.effect {
  background-image: linear-gradient(
    to right,
    #1934b8 0%,
    #239cd8 100%,
    #1934b8 0%
  );
}
</style>

