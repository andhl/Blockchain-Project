<template>
  <div>
    <div>
      <h1>BLOCKCHAIN APP</h1>
    </div>
    <b-container class="bv-example-row">
      <b-row>
        <b-col>
          <ResetBlock @refreshPage="initBlockchain" />
        </b-col>
      </b-row>

      <b-row class="flex-column">
        <b-col v-for="blocks in listOfBlocks" :key="blocks.index">
          <BlockCard
            :blockName="blocks"
            @receive="newHashData"
            @reMine="remineBlock"
          />
        </b-col>
      </b-row>

      <b-row>
        <b-col>
          <AddBlockCard @accept="createNewBlock" />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import ResetBlock from "./ResetBlock.vue";
import BlockCard from "./BlockCard.vue";
import AddBlockCard from "./AddBlockCard.vue";
import { ethers } from "ethers";

export default {
  components: {
    BlockCard,
    AddBlockCard,
    ResetBlock
  },
  data() {
    return {
      listOfBlocks: []
    };
  },
  created() {
    this.initBlockchain();
  },
  methods: {
    initBlockchain() {
      this.listOfBlocks = [];
      this.createNewBlock("Welcome to GBC");
    },
    remineBlock(block) {
      let newHashValue = this.mineBlock(this.listOfBlocks[block.index]);
      this.listOfBlocks[block.index]["hash"] = newHashValue;
      for (let i = block.index + 1; i < this.listOfBlocks.length; i++) {
        this.listOfBlocks[i].previousHash = this.listOfBlocks[i - 1].hash;
        this.listOfBlocks[i].hash = this.hashBlock(this.listOfBlocks[i]);
      }
    },
    newHashData(block) {
      // listOfBlocks[blNumber]["data"] = newData
      let newHashValue = this.hashBlock(this.listOfBlocks[block.index]);
      this.listOfBlocks[block.index]["hash"] = newHashValue;
      for (let i = block.index + 1; i < this.listOfBlocks.length; i++) {
        this.listOfBlocks[i].previousHash = this.listOfBlocks[i - 1].hash;
        this.listOfBlocks[i].hash = this.hashBlock(this.listOfBlocks[i]);
      }
    },
    hashBlock(bl) {
      let input =
        bl.index + bl.previousHash + bl.timestamp + bl.data + bl.nonce;

      return ethers.utils.keccak256("0x" + this.toHex(input));
    },
    mineBlock(bl) {
      let hash = "";
      while (!this.isValidHashDifficulty(hash, 3)) {
        bl["nonce"] = bl["nonce"] + 1;
        let input =
          bl.index + bl.previousHash + bl.timestamp + bl.data + bl.nonce;
        hash = ethers.utils.keccak256("0x" + this.toHex(input));
      }
      return hash;
    },
    createNewBlock(data) {
      let previousHash;
      let index;
      if (this.listOfBlocks.length === 0) {
        previousHash = "0";
        index = 0;
      } else {
        previousHash = this.listOfBlocks.slice(-1)[0].hash;
        index = this.listOfBlocks.slice(-1)[0].index + 1;
      }
      let bl = {
        index: index,
        timestamp: Date.now(),
        data: data,
        previousHash: previousHash,
        nonce: 0
      };

      bl["hash"] = this.mineBlock(bl);
      this.listOfBlocks.push(bl);
    },
    toHex(str) {
      var result = "";
      for (var i = 0; i < str.length; i++) {
        result += str.charCodeAt(i).toString(16);
      }
      return result;
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
@import url("https://fonts.googleapis.com/css?family=Permanent+Marker");

h1 {
  padding-bottom: 20px;
  font-size: 72px;
  font-family: "Permanent Marker", cursive;
  background: -webkit-linear-gradient(rgb(198, 26, 118), rgb(82, 19, 177));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 10px;
}
</style>
