<template>
	<base-card>
		<base-button
			@click="setSelectedTab('stored-resources')"
			:mode="storedResButtonMode"
			>Stored Resources</base-button
		>
		<base-button
			@click="setSelectedTab('add-resources')"
			:mode="addResButtonMode"
			>Add Resource</base-button
		>
	</base-card>
	<keep-alive>
		<component :is="selectedTab"></component>
	</keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResources from './AddResources.vue';
export default {
	components: {
		StoredResources,
		AddResources,
	},
	data() {
		return {
			selectedTab: 'stored-resources',
			storedResources: [
				{
					id: 'official-guide',
					title: 'Official Guide',
					description: 'The official Vue.js documentation',
					link: 'https://vuejs.org/',
				},
				{
					id: 'google',
					title: 'Google',
					description:
						'Google is what you need if you want to play something. ',
					link: 'https://www.google.com/',
				},
			],
		};
	},
	provide() {
		return {
			resources: this.storedResources,
			addResource: this.addResources,
			removeResources: this.removeResources,
		};
	},
	computed: {
		storedResButtonMode() {
			return this.selectedTab === 'stored-resources' ? null : 'flat';
		},
		addResButtonMode() {
			return this.selectedTab === 'add-resources' ? null : 'flat';
		},
	},
	methods: {
		setSelectedTab(tab) {
			this.selectedTab = tab;
		},
		addResources(title, description, link) {
			const newResources = {
				id: new Date().toISOString(),
				title,
				description,
				link,
			};
			this.storedResources.unshift(newResources);
			this.selectedTab = 'stored-resources';
		},
		removeResources(resId) {
			const resIndex = this.storedResources.findIndex((item) => item.id === resId);
			this.storedResources.splice(resIndex, 1);
		},
	},
};
</script>
