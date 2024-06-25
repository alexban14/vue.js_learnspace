<!-- the only rule for a Vue component its that it must have a <template> tag </template> -->
<template>
	<div>
		<!-- <b-jumbotron header="BootstrapVue" lead="Bootstrap v4 Components for Vue.js 2"> -->
		<b-jumbotron>
			<template #lead>
				{{ currentQuestion.question }}
			</template>

			<hr class="my-4">

			<b-list-group>
				<b-list-group-item
					v-for="(answer, index) in answers"
					:key="answer"
					@click="selectAnswer(index)"
					:class="[selectedIndex === index ? 'selected' : '']"
				>
					{{ answer }}
				</b-list-group-item>
			</b-list-group>

			<b-button variant="primary" href="#">Submit</b-button>
			<b-button @click="next" variant="success" href="#">Next</b-button>
		</b-jumbotron>
	</div>
</template>

<script>
import _ from 'lodash';

export default {
  name: 'QuestionBoxComponent',
  // any properties passed to the component will be passed here  
  props: {
	currentQuestion: Object,
	next: Function
  },
  data() {
	return {
		selectedIndex: null,
		shuffledAnswers: {}
	}
  },
  computed: {
	answers() {
		const answers = [...this.currentQuestion.incorrect_answers];
		answers.push(this.currentQuestion.correct_answer);
		return answers
	}
  },
  // methods to be called when props are changing
  watch: {
	currentQuestion: {
		immediate: true,
		handler() {
			this.selectedIndex = null;
			this.shuffleAnswers();
		}
	}
	// correctQuestion() {
	// 	this.selectedIndex = null;
	// 	this.shuffleAnswers();
	// }
  },
  methods: {
	selectAnswer(index) {
		this.selectedIndex = index;
	},
	shuffleAnswers() {
		const answers = [
			...this.currentQuestion.incorrect_answers,
			this.currentQuestion.correct_answer
		];

		this.shuffledAnswers = _.shuffle(answers);
	},
	shuffleArray(array) {
		for (let i = array.length - 1; i > 0; i--) {
			const j = Math.floor(Math.random() * (i + 1));
			const temp = array[i];
			array[i] = array[j];
			array[j] = temp;
		}
	}
  },
  mounted: function() {
	this.shuffleAnswers();
  }
}
</script>

<style scoped>
.list-group {
	margin-bottom: 15px;
}
.list-group-item:hover {
	background: #EEE;
	cursor: pointer;
}
.selected {
	background-color: lightblue;
}
.correct {
	background-color: lightgreen;
}
.incorrect {
	background-color: red;
}
.btn {
	margin: 0 5px;
}
</style>