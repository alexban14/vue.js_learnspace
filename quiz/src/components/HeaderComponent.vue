<!-- the only rule for a Vue component its that it must have a <template> tag </template> -->
<template>
	<div>
		<b-nav>
			<b-nav-item href="#">Fancy Quiz App</b-nav-item>
			<b-nav-item href="#">Counter: {{ numCorrect }}/{{ numTotal }}</b-nav-item>
		</b-nav>
	</div>
</template>

<script>
export default {
	props: [
		'numCorrect',
		'numTotal'
	]
}
</script>