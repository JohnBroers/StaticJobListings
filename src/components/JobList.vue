<template>
    <ul v-if="jobs" class="job__list">
        <JobListItem v-for="job in jobs" :job="job" :key="job.id" />
    </ul>
</template>

<script>
import { computed } from 'vue';
import { useStore } from 'vuex';
import JobListItem from '@/components/JobListItem';
export default {
    components: {
        JobListItem
    },
    setup() {
        const store = useStore();

		store.dispatch('fetchData');
		const jobs = computed(() => store.state.jobsToDisplay);

		return {
			jobs
		}
    }
}
</script>