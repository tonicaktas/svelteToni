<script lang="ts">
	import NamePrice from './NamePrice.svelte'
	import SizeDrop from './SizeDrop.svelte'
	import Description from './Description.svelte'
	import Breadcrumps from './Breadcrumps.svelte'
	import ImageHolder from './ImageHolder.svelte'
	import AddToCart from './AddToCart.svelte'
	import GoogleFont from "@svelte-web-fonts/google";
	import { BarLoader } from 'svelte-loading-spinners'
    import type { GoogleFontDefinition } from "@svelte-web-fonts/google";
	import { onMount } from 'svelte';

	const font: GoogleFontDefinition = {
        family: "Montserrat",
        variants: ["200","300","400"],
    };

	const fetchData = (async () => {
		const data = await fetch('product-data.json').then(res => res.json());
		return await data;
	})()

	let fetchImgs = initailImgs();

    async function initailImgs() {
		let color = '091323-1126'
        const res = await fetch(`https://media.nelly.com/s/nlyscandinavia/${color}.json`)
        const data = await res.json()
        return data
    }

	let fetchPink = pinkImgs();
	let fetchBlue = blueImgs();
	let fetchRed = redImgs();
	

	async function redImgs() {
		let color = '091323-1126'
        const res = await fetch(`https://media.nelly.com/s/nlyscandinavia/${color}.json`)
        const data = await res.json()
        return data
    }

    async function pinkImgs() {
		let color = '091323-0300'
        const res = await fetch(`https://media.nelly.com/s/nlyscandinavia/${color}.json`)
        const data = await res.json()
        return data
    }

	async function blueImgs() {
		let color = '091323-7072'
        const res = await fetch(`https://media.nelly.com/s/nlyscandinavia/${color}.json`)
        const data = await res.json()
        return data
    }
	
</script>

<svelte:head>
	<GoogleFont {font}></GoogleFont>
</svelte:head>

<main>
	<div class="container">
		{#await fetchImgs}
			<BarLoader size="100" color="#FF3E00" unit="px" duration="1s"></BarLoader>
    		{:then res }
			<ImageHolder res={res.items}/>
		{/await} 
		
		<div class="info">
			{#await fetchData}
				<p>Loading JSON</p>
				{:then res }
			
				<Breadcrumps 
					classname={res.ClassName} 
					group={res.GroupName} 
					style={res.StyleName} />
				<NamePrice 
					name={res.Name} 
					brand={res.BrandName} 
					price={res.Price}
					discount={res.Discount}
					ordprice={res.OrdinaryPrice}
					/>
				<SizeDrop size={res.Sizes} soldout={res.SoldOutSizes}/>
				<AddToCart />
				<p class="color-pick">Vald färg: <span>{res.ColorName}</span></p>
			
				<div class="colors-holder">
					{#await fetchRed}
						{:then res }
							{#each res.items as {type, src }, i}
								{#if type === "img" && i === 3 }
									<button style="background:url('{src}')" on:click={() => fetchImgs = redImgs()}></button>
								{/if} 
							{/each}
					{/await} 

					{#await fetchPink}
						{:then res }
							{#each res.items as {type, src }, i}	
								{#if type === "img" && i === 3 }
									<button style="background:url('{src}')" on:click={() => fetchImgs = pinkImgs()}></button>
								{/if} 
							{/each}
					{/await} 

					{#await fetchBlue}
						{:then res }
							{#each res.items as {type, src }, i}
								{#if type === "img" && i === 3 }
									<button style="background:url('{src}')" on:click={() => fetchImgs = blueImgs()}></button>
								{/if} 
							{/each}
					{/await} 
				</div>
				<Description description={res.Description}/>
		
			{/await}
		</div>	
	</div>
</main>

<style type="text/scss">
	main {
		width: 100%;
		font-family: 'Montserrat', sans-serif;
		position: relative;
		padding: 0;

		@media screen and (min-width: 1024px) {
			padding: 15px 0;
		}

		img {
			max-width: 500px;
		}

		.container {
			width: 100%;
			display: flex;
			justify-content: flex-start;
			flex-direction: column;
			align-items: flex-start;
			position: relative;

			@media screen and (min-width: 1024px) {
				flex-direction: row;
				position: relative;
				justify-content: flex-end;
				width: 1140px;
				margin: 70px auto;
				margin: 15px auto;
			}
		}
	}

	.info {
		width: calc(100% - 10px);
		margin: 0 10px;
		position: absolute;
		top: 70vh;

		@media screen and (min-width: 1024px) {		
			width: 35%;
			margin:5px;
			position: relative;
			top: 0;
		}

		.color-pick {
			font-size: .75rem;
        	letter-spacing: 1px;
			color: #adadad;

			span {
				font-weight: 400;
				font-size: .75rem;
				color: #000;
			}
			
		}
		.colors-holder {
			button {
				width: 50px;
				height: 50px;
				border-radius: 50%;
				padding: 2px;

				&:hover {
					cursor: pointer;
				}
				&:focus {
					border: 2px solid #000;
				}
			}
		}
	}
</style>