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

<script lang="js">
    import Vue from "vue";
    import Web3 from "web3";
    import MyContract from '../../../build/contracts/MyContract.json'
    export default {
        data() {
            return {
                contractValue: "",
                contractJson: MyContract,
                currentValue: "",
                isValueUpdated: false,
                loading: ''
            };
        },
        methods: {
            async setValue() {
                this.loading = 'Transaction request is being processed'
                web3 = new Web3(web3.currentProvider)
                let myContract = new web3.eth.Contract(this.contractJson.abi, '0x9828F99985a337c41fE3Ef1B72932365d3EA4e58')
                let setValue = await myContract.methods.set(this.contractValue).send({
                    from: process.env.VUE_APP_ETHADDRESS
                })
                if (setValue) {
                    this.loading = ''
                    this.isValueUpdated = true;
                }
            },
            async getCurrentValue() {
                web3 = new Web3(web3.currentProvider)
                let myContract = new web3.eth.Contract(this.contractJson.abi, '0x9828F99985a337c41fE3Ef1B72932365d3EA4e58')
                let getValue = await myContract.methods.get().call()
                this.currentValue = getValue
            },
        },
        watch: {
            isValueUpdated: function(newValue,oldValue){
                if(newValue == true){
                  window.location.reload(true);
                }
            },
        },
        created: function() {
            this.getCurrentValue()
        }
    };
</script>

<style scoped lang="scss">
    
</style>