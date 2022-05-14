<template>
  <div>
    <div class="flex justify-end m-10">
      <NuxtLink class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" to="/">Home</NuxtLink>
    </div>

    <h1 class="m-10 text-center font-bold text-lg">Transaction: {{ hash }}</h1>
    <div class="grid grid-cols-1 m-10">
      <!-- <div>{{ transaction }}</div> -->
      <div class="bg-gray-300">
          <ul>
            <li>Type: {{ type }}</li>
            <li>Block Number: {{ blockNumber }}</li>
            <li>Block Hash: {{ blockHash }}</li>
            <li>Transaction Index: {{ transactionIndex }}</li>
            <li>To: {{ to }}</li>
            <li>From: {{ from }}</li>
            <li>Confirmations: {{ confirmations }}</li>
            <li>Nonce: {{ nonce }}</li>
          </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { ethers } from "ethers";
const provider = new ethers.providers.JsonRpcProvider(process.env.PROVIDER_URL);

export default {
  name: "Transaction",

  async asyncData(context) {
    const hash = context.query.hash;

    try {
      const transaction = await provider.getTransaction(hash);
      console.log(hash);
      return {
        ...transaction,
      };
    } catch (e) {
      context.error(e);
    }
  },
};
</script>
