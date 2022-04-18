<script setup>
defineProps({
  currentAccount: String
});

const emit = defineEmits(["update:modelValue"]);

async function connectWallet() {
  const { ethereum } = window;
  try {
    if (!ethereum) {
      alert("get metamask");
      return;
    }

    const accounts = await ethereum.request({
      method: "eth_requestAccounts"
    });
    emit("update:modelValue", accounts[0]);
    console.log("accounts", accounts[0]);
  } catch (error) {
    console.log("error", error);
  }
}
</script>
<template>
  <div className="connect-wallet-container">
    <img
      src="https://media.giphy.com/media/3ohhwytHcusSCXXOUg/giphy.gif"
      alt="Erik's donut gif"
    />
    <button @click="connectWallet" className="cta-button connect-wallet-button">
      Connect Wallet
    </button>
  </div>
</template>
