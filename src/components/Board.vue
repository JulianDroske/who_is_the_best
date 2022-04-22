<template>
	<div id="main">
		<div id="topbar">

		</div>
		<div id='main-container'>
			<div id='main-list'>
				<ListView v-for="t in ['good','so','todo']" :key="t" :type="t"
					class="lists">

				</ListView>
			</div>
			<!-- <div id='footer'>

			</div> -->
		</div>
	</div>
</template>

<script>

import ListView from './ListView';

export default {
	name: 'Board',
	components: {
		ListView
	}
}
</script>


<style scoped>
#main {
	display: flex;
	flex-direction: column;
}

#topbar {
	height: 5em;
	/* background: black; */
}

#main-container {
	flex: 1;
	display: flex;
	flex-direction: column;
	max-height: 100%;
	margin: 0 0.5em;
	/* background: yellow; */
}

#main-list {
	flex: 1;
	display: flex;
	flex-direction: row;
	/* background: blue; */
}

#footer {
	margin-top: 1em;
	height: 4em;
	background: red;
}

.lists {
	/* flex: 1; */
	width: calc(100% / 3);
	margin: 1em 0.5em;
}

</style>
