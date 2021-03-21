<template>
	<p v-if="text">{{text}}</p>
</template>
<script>
	export default {
		props: ['text']
	}
</script>