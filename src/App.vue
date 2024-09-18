<script>
import ScrollProgress from '@/components/ScrollProgress.vue'

export default {
	components: {
		ScrollProgress
	}
}

</script>

<template>
	<div id="app">
		<ScrollProgress />
		<router-view />
	</div>
</template>

<style scoped>
#app {
	margin: 40px auto;
}
</style>
