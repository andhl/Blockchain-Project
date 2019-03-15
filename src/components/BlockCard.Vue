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

<style>

</style>
