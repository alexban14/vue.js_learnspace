<template>
	<div class="flex-container">
		<div>
			<p v-once>{{ message }}</p>
			<p v-html="message"></p>
			<p>
				{{ message }}
			</p>
			<!-- 2 way data binding -->
			<input v-model="message">
			<div>
				<div v-if="count === 1">
					Green
				</div>
				<div v-else-if="count === 2">
					Red
				</div>
				<div v-else-if="count === 0">
					Orange
				</div>
			</div>
		</div>
		<div>
			<p>{{ kittify }}</p>
			<input v-model="newCat" v-on:keyup.enter="cats.push(newCat)">
			<button v-on:click="cats.push(newCat)">+ ADD</button>
			<ul id="cats">
				<!-- we can also iterate thru objects or arrays -->
				<li v-for="cat in cats" :key="cat">
					<!-- applying filters -->
					{{ cat | capitalize }}
					<button v-on:click="deleteCat(cat)">Delete</button>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>

export default {
  name: 'BasicsComponent',
  data () {
	return {
		message: '<h1>Salute!</h1>',
		count: 2,
		newCat: '',
		cats: [
			'kitkat',
			'fish',
			'henry',
			'basco',
			'melanthios',
		]
	}
  },
  methods: {
	deleteCat: function(cat) {
		this.cats.splice(this.cats.indexOf(cat), 1);
	}
  },
  filters: {
	capitalize: (value) => value.toUpperCase()
  },
	// updating something rendered in the dom
  computed: {
	kittify: function() {
		if (this.newCat.length < 1) {
			return '';
		}
		return this.newCat + 'y';
	}
  },
	// vue lifecycle methods
  created() {
	console.log('created');
  },
  mounted() {
	console.log('mounted');
  },
  updated() {
	console.log('updated');
  },
  destroyed() {
	console.log('destroyed');
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
 <style scoped>

div {
	margin: 10px;
}

.flex-container {
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
	justify-content: center;
	align-items: center;
	align-content: center
}

button {
	margin: 2px;
	padding: auto;
}
</style>