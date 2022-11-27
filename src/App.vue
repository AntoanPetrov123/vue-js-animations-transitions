<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1 class="text-center">The Super Quiz</h1>
            </div>
        </div>
        <hr>
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <transition :name="effectAnimation" mode="out-in">

                    <!-- here is @answered from quaestion.vue @confirmed is from answer.vue -->
                    <component :is="mode" @answered="answered($event)" @confirmed="mode = 'app-question'"></component>

                </transition>
            </div>
        </div>
    </div>
</template>

<script>
import Question from './components/Question.vue';
import Answer from './components/Answer.vue';

export default {
    data() {
        return {
            mode: 'app-question',
            effectAnimation: 'shake'
        }
    },
    methods: {
        answered(isCorrect) {
            if (isCorrect) {
                this.mode = 'app-answer';
                this.effectAnimation = 'flip';
            } else {
                this.mode = 'app-question';
                // this.effectAnimation = 'shake';
                alert('Wrong, try again!');
            }
            // console.log(this.effectAnimation);
        }
    },
    components: {
        appQuestion: Question,
        appAnswer: Answer
    }
}
</script>

<style>
.flip-enter {
    /* trnasform: rotateY(0deg); */
}

.flip-enter-active {
    animation: flip-in .5s ease-out forwards;
}

.flip-leave {
    /* trnasform: rotateY(0deg); */
}

.flip-leave-active {
    animation: flip-out .5s ease-out forwards;
}

@keyframes flip-out {
    from {
        transform: rotateY(0deg);
    }

    to {
        transform: rotateY(90deg);
    }
}

@keyframes flip-in {
    from {
        transform: rotateY(90deg);
    }

    to {
        transform: rotateY(0deg);
    }
}

.shake-enter {}

.shake-enter-active {
    animation: shake 0.5s infinite;
}

.shake-leave {}

.shake-leave-active {
    animation: shake 0.5s infinite;
}

@keyframes shake {
    0% {
        transform: translate(0);
    }

    20% {
        transform: translate(3em);
    }

    40% {
        transform: translate(-3em);
    }

    60% {
        transform: translate(3em);
    }

    80% {
        transform: translate(-3em);
    }

    100% {
        transform: translate(0);
    }
}
</style>
