<template>
	<ul>
		<LearningResources
			v-for="resource in resources"
			:key="resource.id"
			:resource="resource"
		/>
	</ul>
</template>

<script>
import LearningResources from './LearningResources.vue';
export default {
	inject: ['resources'],
	components: { LearningResources },
};
</script>

<style scoped>
ul {
	list-style: none;
	margin: 0;
	padding: 0;
	margin: auto;
	max-width: 40rem;
}
</style>
