<script setup>
import { onMounted, ref } from "vue";
import Layout from "./components/layout.vue";
import NotConnectedForm from "./components/not-connected-form.vue";
import InputForm from "./components/input-form.vue";

const currentAccount = ref();

async function checkIfWalletIsConnected() {
  const { ethereum } = window;

  if (!ethereum) {
    console.log("error");
    return;
  } else {
    console.log("we have an ethereum object", ethereum);
  }

  const accounts = await ethereum.request({ method: "eth_accounts" });

  if (accounts.length !== 0) {
    const account = accounts[0];
    currentAccount.value = account;
  } else {
    console.log("no authorized accounts");
  }
}

onMounted(() => {
  checkIfWalletIsConnected();
});
</script>

<template>
  <layout>
    <not-connected-form v-model="currentAccount" v-if="!currentAccount" />
    <input-form v-if="currentAccount" />
  </layout>
</template>

<style>
@import "./assets/base.css";
</style>
