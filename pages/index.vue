<template>
  <div>
    <h1 class="m-10 text-center font-bold text-lg">Ethereum Block Explorer</h1>
    <div class="flex justify-center">
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="refresh">Refresh</button>
    </div>
    <div class="grid grid-cols-2 gap-4 m-10">
      <div id="latest-block" class="bg-gray-300">
          <ul>
            <li>Block Number: {{ number }}</li>
            <li>Block Hash: {{ hash }}</li>
            <li>Transaction Count: {{ transactions.length }}</li>
            <li>Nonce: {{ nonce }}</li>
            <li>Gas Used: {{ gasUsed.toString() }}</li>
          </ul>
      </div>
      <div class="bg-gray-300">
        <ul id="latest-transactions">
          <li v-for="transaction in firstTenTransactions" v-bind:key="transaction">
            <NuxtLink v-bind:to="{ path: 'transaction', query: { hash: transaction}}" class="hover:underline">{{ transaction }}</NuxtLink>
          </li>
        </ul>
        <h1>...</h1>
        <h1>Transaction Total: {{ transactions.length }}</h1>
      </div>
    </div>
  </div>
</template>

<script>
import { ethers } from "ethers";

console.log(process)
const provider = new ethers.providers.JsonRpcProvider(
  process.env.PROVIDER_URL
);

export default {
  name: "IndexPage",

  async asyncData() {
    const blockNumber = await provider.getBlockNumber();
    const blockData = await provider.getBlock(blockNumber);
    console.log(blockData);
    return {
      ...blockData,
      firstTenTransactions: blockData.transactions.splice(0, 10)
    };
  },

  methods: {
    refresh() {
      this.$nuxt.refresh();
    },
  },

  computed: {
    transactionHtml() {
      return this.transactions.splice(0, 10).reduce((string, tx) => {
        return string+`<li>${tx}</li>`
      }, '');
    }
  }
};
</script>
