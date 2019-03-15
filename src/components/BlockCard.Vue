<template>
  <div class="card-box">
    <b-card class="card-content">
      <b-card-text>
        <span class="text1">DATA</span>
        <input
          type="text"
          class="input-line"
          v-model="blockName.data"
          @input="changedData"
        />
      </b-card-text>
      <b-card-text class="text1">
        PREVIOUS HASH
        <span
          class="hashFont"
          :class="
            isValidHashDifficulty(blockName.previousHash, 3) ||
            blockName.previousHash == 0
              ? 'green'
              : 'red'
          "
          >{{ blockName.previousHash }}</span
        >
      </b-card-text>
      <b-card-text class="text1">
        HASH
        <span
          class="hashFont"
          :class="isValidHashDifficulty(blockName.hash, 3) ? 'green' : 'red'"
          >{{ blockName.hash }}</span
        >
      </b-card-text>
      <b-card-text class="textField text1">
        <span>Block#</span>
        {{ blockName.index }}
        <span class="dateProp">on {{ dateCreated }}</span>
      </b-card-text>

      <div class="nonceMine">
        <b-card-text
          class="nonceMineShell"
          v-if="isValidHashDifficulty(blockName.hash, 3)"
          >{{ blockName.nonce }}</b-card-text
        >
        <b-button
          v-else
          class="button effect pulse"
          @click="mineNewHash"
        ></b-button>
      </div>
    </b-card>
  </div>
</template>

<script>
import moment from "moment";
export default {
  props: {
    blockName: Object
  },
  computed: {
    dateCreated() {
      return moment(this.blockName.timestamp).format("MMMM Do YYYY, h:mm:ss a");
    }
  },
  methods: {
    mineNewHash() {
      this.$emit("reMine", this.blockName);
    },
    changedData() {
      this.$emit("receive", this.blockName);
    },
    isValidHashDifficulty(hash, difficulty) {
      hash = hash.substring(2);
      for (var i = 0, b = hash.length; i < b; i++) {
        if (hash[i] !== "0") {
          break;
        }
      }
      return i >= difficulty;
    }
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Orbitron");
@import url("https://fonts.googleapis.com/css?family=Kanit");
@import url("https://fonts.googleapis.com/css?family=Exo:800");
@import url("https://fonts.googleapis.com/css?family=PT+Serif");

.hashFont {
  font-family: "Kanit", sans-serif;
  font-size: 13px;
  padding-left: 10px;
}

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

.dateProp {
  padding-left: 5px;
  font-size: 10px;
  font-family: "PT Serif", serif;
}

.nonceMine {
  display: inline-block;
  float: right;
  padding-bottom: 15px;
}

.nonceMineShell {
  border: 0;
  padding: 2px;
  border-color: none;
  border-radius: 5px;
  background: rgba(16, 101, 144, 0.08);
  color: transparent;
  text-shadow: 0 0 0 rgb(175, 16, 167);
}

.red {
  color: red;
}

.green {
  color: green;
}

.text1 {
  font-family: "Exo", sans-serif;
  font-size: 1.1rem;
}

.card-box {
  width: 60%;
  margin-left: auto;
  margin-right: auto;
  padding-bottom: 5%;
}

.card-content {
  display: inline-block;
  text-align: left;
  border-width: thin;
  border-color: rgb(217, 232, 238);
  border-radius: 10px;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  font-size: 0.9rem;
  color: #339ca2;
  transition: box-shadow 0.4s;
  box-shadow: 0px 5px 10px rgba(133, 143, 147, 0.8);
  width: 100%;
}

.card-content:hover {
  box-shadow: 0px 30px 80px rgba(133, 143, 147, 0.5);
}

input {
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
  width: 90%;
}

.input-line:focus {
  outline: none;
}

.button {
  float: right;
  border-color: transparent;
  color: transparent;
  padding: 18px;
  text-align: center;
  color: white;
  border-radius: 50%;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 0.75rem;
}

.effect {
  background-image: url("../assets/miner.png"),
    linear-gradient(to right, #1934b8 0%, #239cd8 100%, #1934b8 0%);
  background-repeat: no-repeat;
  background-position: center;
}
</style>
