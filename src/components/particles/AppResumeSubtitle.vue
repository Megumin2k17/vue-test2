<template>
	<h2 v-if="subtitle">{{subtitle}}</h2>
</template>
<script>
	export default {
		props: ['subtitle']
	}
</script>