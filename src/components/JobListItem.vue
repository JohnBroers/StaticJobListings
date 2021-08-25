<template>
    <li class="job" :class="{ 'job--featured' : job.featured}">
        <figure class="job__logo-wrapper">
            <img :src="fixImagePath(job.logo)" :alt="job.company" class="job__logo">
        </figure>
        <div class="job__head">
            <div class="job__title">
                <span class="job__company">{{ job.company }}</span>
                <span v-if="job.new" class="job__label job__label--new">New!</span>
                <span v-if="job.featured" class="job__label job__label--featured">Featured</span>
            </div>
            <div class="job__info">
                <p class="job__position">{{ job.position }}</p>
                <p class="job__metaitems">
                    <span class="job__metaitem">{{ job.postedAt }}</span>
                    <span class="job__metaitem">{{ job.contract }}</span>
                    <span class="job__metaitem">{{ job.location }}</span>
                </p>
            </div>
        </div>
        <div class="job__tags">
            <button class="job__tag" @click="filterClick(tag)" v-for="tag in job.filterOptions" :key="tag">{{ tag }}</button>
        </div>
    </li>
</template>

<script>
import { useStore } from 'vuex';

export default {
    props: {
        job: {
            type: Object,
            required: true
        }
    },
    emits: ['filterClick'],
    setup() {
        const store = useStore();

        function fixImagePath(src) {
            const path = src.replace('./', '');
            return require(`@/assets/${path}`);
        }

        function filterClick(name) {
            store.commit('toggleFilter', name);
        }

        return {
            fixImagePath,
            filterClick
        }
    },
}
</script>