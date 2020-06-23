<template lang="html">
	<div id="sightingsGrid">
		<sighting v-for="(sighting, index) in sightings" :sighting="sighting" :key="index"/>
	</div>
</template>

<script>
import {eventBus} from '@/main.js'
import SightingService from '@/services/SightingService.js'
import Sighting from './Sighting.vue';

export default {
	name: 'sightings-grid',
	components: {
		'sighting': Sighting
	},
	// props: ['sightings'],
	data(){
		return{
			sightings: []
		};
	},
	mounted(){
		SightingService.getSightings()
		.then(sightings => this.sightings = sightings);

		eventBus.$on('sighting-added', (sighting) =>{
			this.sightings.push(sighting)
		})

		eventBus.$on('delete-sighting', (sighting) =>{
			this.sightings.splice(index, 1)
		})
	}
}

</script>

<style lang="css" scoped>
#sightingsGrid {
	display: flex;
	flex-wrap: wrap;
	justify-content: space-evenly;
}

h2 {
	padding: 0;
	margin: 0;
}
</style>
