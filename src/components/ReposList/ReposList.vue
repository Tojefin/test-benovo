<script>
export default {
	props: {
		repos: {
			type: Array,
			default: function () {
				return []
			}
		},
		type: {
			validator: function (value) {
				return ['search', 'liked'].includes(value)
			}
		}
	},
	methods: {
		save(repo) {
			console.log(repo)
			let storage = JSON.parse(localStorage.getItem("liked"))
			if (!storage) {
				storage = []
			}
			if (storage.filter((r) => r.id == repo.id).length) return
			storage.unshift(repo)
			localStorage.setItem("liked", JSON.stringify(storage))
			this.$emit('update')
		},
		remove(repo) {
			let storage = JSON.parse(localStorage.getItem("liked"))
			localStorage.setItem("liked", JSON.stringify(storage.filter((r) => r.id != repo.id)))
			this.$emit('update')
		}
	}
}
</script>

<template>
	<ul v-if="repos.length">
		{{ type == 'search' ? 'Найдено' : 'Сохранено' }} {{ repos.length }}
		<li v-for="repo in repos" :key="repo.id">
			<div class="box">
				<div class="info">
					<h3>
						<div class="avatar"><img width="20" height="20" :src="repo.owner.avatar_url" alt=""></div>
						<div class="title"><a :href="`repo?r=${repo.full_name}`">{{ repo.full_name }}</a></div>
					</h3>
					<div class="desc">
						<span>{{ repo.description }}</span>
					</div>
					<div class="stats">
						<div class="stat">⭐ {{ repo.stargazers_count }}</div>
						<span aria-hidden="true">·</span>
						<div class="stat">ψ {{ repo.forks_count }}</div>
					</div>
				</div>
				<div class="action">
					<button v-if="type == 'search'" @click="() => save(repo)" title="Сохранить">⭐</button>
					<button v-if="type == 'liked'" @click="() => remove(repo)" title="Удалить">❌</button>
				</div>
			</div>
		</li>
	</ul>
</template>



<style scoped src="./style.css">