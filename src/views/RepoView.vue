<script>
export default {
	data: function () {
		return {
			repo: {},
		}
	},
	methods: {
		getRepo: async function () {
      this.$route.query.r

			const res = await fetch(`https://api.github.com/repos/${this.$route.query.r}`)
			this.repo = await res.json()
		},
	},
	mounted: function () {
		this.getRepo()
	}
}
</script>

<template>
	<main>
    <a href="/">Назад</a>
    <h2>{{ repo.full_name }}</h2>
    <pre>{{ repo }}</pre>
	</main>
</template>

<style scoped>
main {
	display: flex;
	flex-direction: column;
	gap: 32px;
}

div {
	display: flex;
	gap: 32px;
}
</style>
