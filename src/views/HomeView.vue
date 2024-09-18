<script>
import SearchForm from '@/components/SearchForm.vue'
import ReposList from '@/components/ReposList/ReposList.vue'
import CopySearch from '@/components/CopySearch.vue'

export default {
	components: {
		SearchForm,
		ReposList,
		CopySearch
	},
	data: function () {
		return {
			searched: [],
			liked: [],
			searchText: ''
		}
	},
	methods: {
		search: async function (keywords) {
			this.searchText = keywords
			if (!keywords.length) return

			const res = await fetch(`https://api.github.com/search/repositories?q=${keywords}`)
			const { items } = await res.json()
			this.searched = items
		},
		loadSaved: function () {
			let storage = JSON.parse(localStorage.getItem("liked"))
			if (!storage) {
				storage = []
			}
			this.liked = storage
		}
	},
	mounted: function () {
		this.loadSaved()
	}
}
</script>

<template>
	<main>
		<div>
			<SearchForm v-on:input="search" />
			<CopySearch :text="searchText" />
		</div>
		<div>
			<ReposList :repos="searched" :type="'search'" @update="loadSaved" />
			<ReposList :repos="liked" :type="'liked'" @update="loadSaved" />
		</div>
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
