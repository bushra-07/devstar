<!-- CSS Hover Effect Generator by Rishabh Rai --Start -->
<script>
	import { onMount } from 'svelte';

	let backgroundColor = '#3498db';
	let hoverColor = '#ff0000';
	let scale = 1;
	let rotation = 0;

	const updateCSSCode = () => `
	.hover-effect {
		background-color: ${backgroundColor};
		transition: all 0.3s ease;
		transform: scale(${scale}) rotate(${rotation}deg);
	}

	.hover-effect:hover {
		background-color: ${hoverColor};
		transform: scale(${scale}) rotate(${rotation}deg);
	}
	`;

	const copyText = () => {
		const cssCode = updateCSSCode();
		navigator.clipboard.writeText(cssCode)
		.then(() => console.log("CSS copied to clipboard"))
		.catch(err => console.error("Error copying CSS:", err));
	};

	const downloadFile = () => {
	const cssCode = updateCSSCode();
	const blob = new Blob([cssCode], { type: 'text/css' });
	const url = URL.createObjectURL(blob);
	const a = document.createElement('a');
	a.href = url;
	a.download = 'hover-effect.css';
	a.click();
	URL.revokeObjectURL(url);
	};
	const randomizeColors = () => {
	  backgroundColor = '#' + Math.floor(Math.random() * 16777215).toString(16);
	  hoverColor = '#' + Math.floor(Math.random() * 16777215).toString(16);
	};
	onMount(updateCSSCode);
</script>
<div class="w-full max-w-3xl mx-auto p-8 bg-white rounded-lg shadow-md dark:bg-gray-800 grid grid-cols-1 md:grid-cols-2 gap-15">
	<h1 class="col-span-2 text-2xl font-bold text-center mb-8 dark:text-white md:col-span-2">CSS Hover Effect Generator</h1>
	<!-- Left Side: Form Elements -->
	<div class="space-y-6">
		<div class="mt-4">
			<div class="flex space-x-2 items-center gap-20" >
				<div>
					<span class="text-sm font-medium block text-gray-700 dark:text-gray-400 mb-1.5">Background:</span>
					<input type="color" bind:value={backgroundColor} class="mt-1 w-full h-10 border rounded"/>
				</div>
				<div>
					<span class="text-sm font-medium block text-gray-700 dark:text-gray-400 mb-1.5">Hover Color:</span>
					<input type="color" bind:value={hoverColor} class="mt-1 w-full h-10 border rounded"/>
				</div>
			</div>
		</div>
		
		<div>
			<span class="text-sm font-medium block text-gray-700 dark:text-gray-400 mb-1">Scale: <span class="ml-2">{scale}</span></span>
			<input type="range" min="1" max="2" step="0.1" bind:value={scale} class="w-80 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"/>
		</div>
		
		<div>
			<span class="text-sm font-medium block text-gray-700 dark:text-gray-400 mb-1">Rotation (degrees): <span class="ml-2">{rotation}</span></span>
			<input type="range" min="0" max="360" step="10" bind:value={rotation} class="w-80 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"/>
		</div>
	</div>
	
	<div class="flex items-center justify-center">
		<div 
		class="border p-8 rounded-lg transition-all duration-300 hover-effect flex items-center justify-center text-white font-bold text-2xl"
		style="background-color: {backgroundColor}; transform: scale(${scale}) rotate(${rotation}deg);"
		on:mouseover={() => {
			document.querySelector('.hover-effect').style.backgroundColor = hoverColor;
			document.querySelector('.hover-effect').style.transform = `scale(${scale}) rotate(${rotation}deg)`;
		}}
			on:mouseout={() => {
				document.querySelector('.hover-effect').style.backgroundColor = backgroundColor;
				document.querySelector('.hover-effect').style.transform = 'none';
			}}>
			Hover me!
		</div>
	</div>
	<div class="col-span-2 grid grid-cols-3 px-7 pt-10 gap-10">
		<button type="button" class="text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-5 py-2.5 w-full dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800" on:click={randomizeColors}>Random Colors</button>
		<button type="button" class="text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-5 py-2.5 w-full dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800" on:click={copyText}>Copy CSS</button>
		<button type="button" class="text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-5 py-2.5 w-full dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800" on:click={downloadFile}>Download CSS</button>
	</div>
</div>
<style>
	.hover-effect {
		transition: all 0.3s ease;
	}
</style>
<!-- CSS Hover Effect Generator by Rishabh Rai --End -->
