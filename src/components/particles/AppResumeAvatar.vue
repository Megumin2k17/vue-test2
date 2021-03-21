<template>	
	<div class="avatar" v-if="avatar">
        <img :src="avatar">
    </div>
</template>
<script>
	export default {
		props: ['avatar']
	}
</script>