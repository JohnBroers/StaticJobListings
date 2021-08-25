<template>
	<header>
		<h1>Static Job Listing</h1>
	</header>
	<main class="main">
		<JobFilter />
		<JobList />
	</main>
</template>

<script>
import JobList from '@/components/JobList';
import JobFilter from '@/components/JobFilter';

export default {
	name: 'App',
	components: {
		JobList,
		JobFilter
	}
}
</script>

<style lang="scss">
@import '@/assets/scss/index.scss';
</style>