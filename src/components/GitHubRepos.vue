<template>
    <div>
        <!-- TODO: Crear componente GitHubRepos -->
        <div v-for="(item, id) in repolist" :key="id">
                {{ item.full_name}}
                {{ item.forks_count }} <img src="imagen_fork.png" style="width:8px">
        </div>
    </div>
</template>

<script>
export default {
    name: 'GitHubRepos',
    props: [
        // TODO: crear parámetro 'repolist'
        'repolist'
    ],
}
</script>

<style scoped>
</style>
