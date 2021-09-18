<template>
    <div>
        <b-jumbotron>
            <template >
               <div class="mt-5">
                   {{ cquestion.question }}
               </div>
            </template>

            <hr class="my-4">

            <b-list-group 
                v-for="(answer, i) in shuffledAnswers" 
                :key="i"
                @click="ChangeIndex(i)" 
                >
                <b-list-group-item :class="correctFunc(i)">
                    {{ i+1 }} {{answer}}
                </b-list-group-item>
            </b-list-group>

            <b-button 
                variant="primary" 
                @click="submitAnswer"
                :disabled="cindex === null || answered"
                href="#">Submit</b-button>
            <b-button variant="success" href="#" @click="next">Next</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
    import _ from 'lodash'
    export default {
        props: {
            cquestion: Object,
            next: Function,
            increment: Function,
        },
        data(){
            return {
                cindex: null,
                shuffledAnswers: [],
                correctAnswer: null,
                answered: false
            }
        },
        methods: {
            ChangeIndex(i){
                this.cindex = i;
                console.log(i);
            },
            shuffleAnswers(){
               let answers = [ ...this.cquestion.incorrect_answers, this.cquestion.correct_answer ];
               this.shuffledAnswers = _.shuffle(answers);
               this.correctAnswer = this.shuffledAnswers.indexOf(this.cquestion.correct_answer);
            },
            submitAnswer(){
                let is_correct = false;
                if(this.cindex === this.correctAnswer) {
                    is_correct = true;
                }
                this.answered = true;
                this.increment(is_correct);
            },
            correctFunc(i){

                let answerClass = '';

                if(!this.answered && this.cindex === i){
                    answerClass = 'selected';
                }else if(this.answered && i === this.correctAnswer){
                    answerClass = 'correct';
                }else if(this.answered && i === this.cindex && i !== this.correctAnswer){
                    answerClass = 'incorrect';
                }

                return answerClass;
            }
            
        },
        computed: {
            answers(){
                let answers = [...this.cquestion.incorrect_answers];
                answers.push(this.cquestion.correct_answer);
                return answers;
            }
        },
        watch: {
            cquestion: {
                immediate: true,
                handler(){
                    this.cindex = null;
                    this.answered = null;
                    this.correctAnswer = null;
                    this.shuffleAnswers();
                }
            }
        }
    }
</script>

<style scoped>
    .list-group-item:hover {
        background-color: #eee;
        cursor: pointer;
    }
    .btn{
        margin: 10px 2px;
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
</style>