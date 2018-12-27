<template>
  <div class="container">
    <h1>Here is the value stored on the blockchain: {{currentValue}}</h1>
    <b-field label="Update the value">
      <b-input size="is-small" class="setValue" v-model="contractValue"></b-input>
    </b-field>
    <h1>{{loading}}</h1>
    <button class="button is-primary" @click="setValue">Update</button>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop, Watch } from "vue-property-decorator";
import Web3 from "web3";
const MyContract = require("../../build/contracts/MyContract.json");

@Component
export default class HelloWorld extends Vue {
  contractValue: string = "";
  currentValue: string = "";
  loading: string = "";
  isValueUpdated: boolean = false;

  async setValue() {
    this.loading = "Transaction request is being processed";
    // @ts-ignore
    web3 = new Web3(web3.currentProvider);
    // @ts-ignore
    let myContract = new web3.eth.Contract(
      MyContract.abi,
      "0x9828F99985a337c41fE3Ef1B72932365d3EA4e58"
    );
    let setValue = await myContract.methods.set(this.contractValue).send({
      from: process.env.VUE_APP_ETHADDRESS
    });
    if (setValue) {
      this.loading = "";
      this.isValueUpdated = true;
    }
  }

  async getCurrentValue() {
    // @ts-ignore
    web3 = new Web3(web3.currentProvider);
    // @ts-ignore
    let myContract = new web3.eth.Contract(
      MyContract.abi,
      "0x9828F99985a337c41fE3Ef1B72932365d3EA4e58"
    );

    let getValue = await myContract.methods.get().call();
    this.currentValue = getValue;
  }

  @Watch("isValueUpdated")
  onPropertyChanged(newValue: boolean, oldValue: boolean) {
    if (newValue == true) {
      window.location.reload(true);
    }
  }
  mounted() {
    this.getCurrentValue();
  }
}
</script>

<style scoped lang="scss">
</style>
