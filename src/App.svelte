<script>
	import Header from "./components/Header.svelte"
	import Footer from "./components/Footer.svelte"
	import Tabs from "./shared/Tabs.svelte"

	// Tabs
	let items = ['Current Polls', "Add New Poll"]
	let activeItem = "Current Polls"
	const tabUpdate = (e) => {
		activeItem = e.detail;
		
	}
</script>

<Header />
<main>
	<Tabs {items} {activeItem} on:tabChange={tabUpdate} />
	{#if activeItem === 'Current Polls'}
	  <p>Poll list component here</p>
	  {:else if activeItem === 'Add New Poll' }
	  <p>New poll form goes here</p>
	{/if}
</main>
<Footer />
<style>
	main {
		max-width: 960px;
		margin: 40px auto;
	}
</style>