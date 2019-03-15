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

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Orbitron");
@import url("https://fonts.googleapis.com/css?family=Exo:800");

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

.text {
  font-family: "Exo", sans-serif;
  padding: 10px 0 20px 0;
  font-size: 1.1rem;
}

.group-box {
  box-sizing: border-box;
}

.card-box {
  width: 30%;
  margin-left: auto;
  margin-right: auto;
  padding-bottom: 30px;
}

.card-content {
  border-width: thin;
  border-color: rgb(217, 232, 238);
  border-radius: 10px;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  font-size: 0.9rem;
  color: #339ca2;
  transition: box-shadow 0.4s;
  box-shadow: 0px 5px 10px rgba(133, 143, 147, 0.8);
}

.card-content:hover {
  box-shadow: 0px 30px 80px rgba(133, 143, 147, 0.5);
}

input {
  box-shadow: 0px 0px 1px rgba(133, 143, 147);
  margin-left: 5px;
  width: 80%;
}

.input-line {
  border: 0;
  border-color: none;
  border-radius: 5px;
  background: rgba(16, 101, 144, 0.08);
  color: transparent;
  text-shadow: 0 0 0 rgb(175, 16, 167);
  font-family: "Orbitron", sans-serif;
  font-size: 15px;
  padding-left: 10px;
  font-size: 15px;
}

.input-line:focus {
  outline: none;
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
