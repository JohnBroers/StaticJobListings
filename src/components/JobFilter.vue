<template>
    <section class="filter" v-if="filters.length">
        <section class="filter__taglist">
            <span class="filter__tag" v-for="option in filters" :key="option"> 
                <span class="filter__tag-text">{{ option }}</span>
                <button class="filter__tag-remove" @click="removeFilter(option)">&#10005;</button>
            </span>
        </section>
        <div class="filter__actions">
            <button class="filter__clear" @click="clearFilters">Clear</button>
        </div>
    </section>
</template>

<script>
import { watch, computed } from 'vue';
import { useStore } from 'vuex';

export default {
    setup() {
        const store = useStore();
        const filters = computed(() => store.state.filters);

        function removeFilter(val) {
            store.commit('toggleFilter', val);
        }

        function clearFilters() {
            store.commit('clearFilter');
        }

        watch(filters, () => {
            store.commit('filtersJobs');
        },{ deep: true })

        return {
            filters,
            removeFilter,
            clearFilters
        }
    }
}
</script>