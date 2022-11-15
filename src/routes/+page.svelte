<script>
	import DetailsMerchant from './DetailsMerchant.svelte';
</script>

<svelte:head>
	<title>Merchants</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<DetailsMerchant />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}
</style>
