<template>
  <div class="container">
    <background src="../assets/diceGif.gif" />
    <div class="text-center pt-12">
      <h1 class="content">
            <h2>THE DICE SHOP</h2>
            <h2>THE DICE SHOP</h2>

      </h1>
      <div style="margin-top:10%" v-if="walletStore.address != ''">
        <button class="button" @click="() => mintNFTHandler">Mint</button>
      </div>
      <p style="margin-top:10%" v-else>You've not connected your wallet yet</p>
    </div>
    
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { useWalletStore } from '../stores/wallet';
import { ethers } from 'ethers';



// Contract ABI
import MessagePortal from '../contracts/NFTCollectible.json';
import { log } from 'console';
const contractAddress = '0x5809689c338EBebe4f0f9FDA95dFD89E8996Da24';

export default defineComponent({
  name: 'WaveMe',

  components: {},


  setup() {
    const walletStore = useWalletStore();
    return {
      walletStore,
    };
  },
  mounted() {


  },
  //   watch: {
  //   '$store.': {
  //     handler() {
  //       this.getTodo();
  //     },
  //     immediate: true
  //   } 
  // },
  computed: {

    mintNFTHandler: async function () {

      if (typeof window.ethereum !== 'undefined') {
        const provider = new ethers.providers.Web3Provider(window.ethereum);
        const signer = provider.getSigner();
        // Contract reference
        const nftContract = new ethers.Contract(
          contractAddress,
          MessagePortal.abi,
          signer
        );

        console.log("Initialize payment....");
        let nftTxn = await nftContract.mintNFTs(1, { value: ethers.utils.parseEther("0.01") });

        console.log(`Mined, see at : https://rinkeby.etherscan.io/tx/${nftTxn.hash}`);
        alert(`Mined, see at : https://rinkeby.etherscan.io/tx/${nftTxn.hash}`)
      }
      else {
        console.log("Etherum obj does not exist")
      }
    }


  },
  watch: {

  },
});
</script>
<style>
@import url("https://fonts.googleapis.com/css?family=Poppins:100,200,300,400,500,600,700,800,900");
.container {
  background-image:  url(../assets/diceGif.gif);
  width: 100%;
  height: 100%;
  background-size: contain;
}
.button {
 padding: 17px 60px;
 border-radius: 50px;
 /* border: 0; */
 background-color: white;
 box-shadow: rgb(0 0 0 / 5%) 0 0 8px;
 letter-spacing: 1.5px;
 text-transform: uppercase;
 font-size: 15px;
 transition: all .5s ease;
 border: 3px solid hsl(261deg 80% 48%) ;
 /* font-weight: none !important; */
}

button:hover {
 letter-spacing: 3px;
 background-color: hsl(261deg 80% 48%);
 color: hsl(0, 0%, 100%);
 box-shadow: rgb(93 24 220) 0px 7px 29px 0px;
}

button:active {
 letter-spacing: 3px;
 background-color: hsl(261deg 80% 48%);
 color: hsl(0, 0%, 100%);
 box-shadow: rgb(93 24 220) 0px 0px 0px 0px;
 transform: translateY(10px);
 transition: 100ms;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

.content {
  margin-top: 50px;
  position: relative;
   align-items: center;
  justify-content: center;
  font-weight: 700;
}

.content h2 {
 
  color: #fff;
  font-size: 8em;
  position: absolute;
  transform: translate(30%, -50%);
}

.content h2:nth-child(1) {
  color: transparent;
  -webkit-text-stroke: 2px hsl(261deg 80% 48%);
}

.content h2:nth-child(2) {
  color: hsl(261deg 80% 48%);
  animation: animate 4s ease-in-out infinite;
}

@keyframes animate {
  0%,
  100% {
    clip-path: polygon(
      0% 45%,
      16% 44%,
      33% 50%,
      54% 60%,
      70% 61%,
      84% 59%,
      100% 52%,
      100% 100%,
      0% 100%
    );
  }

  50% {
    clip-path: polygon(
      0% 60%,
      15% 65%,
      34% 66%,
      51% 62%,
      67% 50%,
      84% 45%,
      100% 46%,
      100% 100%,
      0% 100%
    );
  }
}
</style>
