<script lang="ts">
	export let name: string;

	import { ethers, WalletConnectProvider, Web3Modal } from "./utils";

	// import WalletConnectProvider from "@walletconnect/web3-provider";
	// import Web3Modal from "web3modal";
	// import { ethers } from "ethers";
	import { onMount } from 'svelte';

	const providerOptions = {
		walletconnect: {
			package: WalletConnectProvider,
			options: {
			infuraId: "795587fc9545486b8a5e190a44e3ae7d",
			},
		},
	};

	const web3Modal = new Web3Modal({
		network: "mainnet", // optional
		cacheProvider: true, // optional
		providerOptions // required
	});

	onMount(async () => {
		const instance = await web3Modal.connect();
		// const instance = await web3Modal.connectTo("walletconnect");
		// web3Modal.connect().then(console.log);
		// const res = await fetch(`/tutorial/api/album`);
		// photos = await res.json();
		const provider = new ethers.providers.Web3Provider(instance);

		// Subscribe to accounts change
		// provider.on("accountsChanged", (accounts: string[]) => {
		// 	console.log(accounts);
		// });

		// // Subscribe to chainId change
		// provider.on("chainChanged", (chainId: number) => {
		// 	console.log(chainId);
		// });

		// // Subscribe to provider connection
		// provider.on("connect", (info: { chainId: number }) => {
		// 	console.log(info);
		// });

		// // Subscribe to provider disconnection
		// provider.on("disconnect", (error: { code: number; message: string }) => {
		// 	console.log(error);
		// });


		const signer = provider.getSigner();
		console.log(signer);
		console.log(await signer.getAddress());
	});

</script>

<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>