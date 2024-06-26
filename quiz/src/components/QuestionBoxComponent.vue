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
					v-for="(answer, index) in shuffledAnswers"
					:key="answer"
					@click="selectAnswer(index)"
					:class="answerClass(index)"
				>
					{{ answer }}
				</b-list-group-item>
			</b-list-group>

			<b-button
				variant="primary"
				@click="submitAnswer"
				:disabled="selectedIndex === null || answered"
			>
				Submit
			</b-button>
			<b-button @click="next" variant="success">
				Next
			</b-button>
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
	next: Function,
	increment: Function
  },
  data() {
	return {
		selectedIndex: null,
		shuffledAnswers: {},
		answered: false,
		correctIndex: null
	}
  },
  computed: {
	answers() {
		const answers = [...this.currentQuestion.incorrect_answers];
		answers.push(this.currentQuestion.correct_answer);
		console.log(answers);
		return answers
	}
  },
  // methods to be called when props are changing
  watch: {
	currentQuestion: {
		immediate: true,
		handler() {
			this.selectedIndex = null;
			this.answered = false;
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
	submitAnswer() {
		let isCorrect = false;

		if (this.shuffledAnswers[this.selectedIndex] === this.currentQuestion.correct_answer) {
			isCorrect = true;
		}
		this.answered = true;

		this.increment(isCorrect);
	},
	shuffleAnswers() {
		const answers = [
			...this.currentQuestion.incorrect_answers,
			this.currentQuestion.correct_answer
		];

		this.shuffledAnswers = _.shuffle(answers);
		this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
	},
	answerClass(index) {
		let answerClass = '';

		if (!this.answered && this.selectedIndex === index) {
			answerClass = 'selected';
		} else if (this.answered && this.correctIndex === index) {
			answerClass = 'correct';
		} else if (
			this.answered && 
			this.selectedIndex === index &&
			this.correctIndex !== index
		) {
			answerClass = 'incorrect';
		}

		return answerClass;
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