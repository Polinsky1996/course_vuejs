<template>
    <label 
    :for="`key-${index}`"
    :class="style"
    class="card_label">
        <input 
        @click="setAnswer" 
        :id="`key-${index}`"
        :value="index"
        v-model="selected"
        :disabled="haveAnswer"
        class="card_custom-checkbox"
        type="radio">    
        {{option}}
    </label>
</template>

<script>
export default {
    props: {
        option: {
            type: String,
            require: false
        },

        correctAnswer: {
            type: Number,
            require: false
        },

        index: {
            type: Number,
            require: false
        },

        haveAnswer: {
            type: Boolean
        }
    },

    data() {
        return {
            selected: null
        }
    },

    methods: {
        setAnswer() {
            this.$emit('setAnswer', this.index);
        }
    },

    watch: {    
        option() {
            this.selected = null;
        }
    },


    computed: {
        style() {
            const styleAnswer = [];

            if (this.haveAnswer) {
                if (this.selected != null) {
                    styleAnswer.push('selected');

                    if (this.correctAnswer == this.index) {
                        styleAnswer.push('correct')
                    } else {
                        styleAnswer.push('incorrect')
                    } 

                }
                else {
                    styleAnswer.push('unselected');
                }    
            }

            return styleAnswer;
        }
    }
}
</script>

<style scoped>
.card_label {
    padding: 10px 50px;
    margin: 5px;
    
    background-color: #574f7d;
    border-radius: 7px;
    border: 4px solid #95adbe;
    cursor: pointer;

    font-size: 1.5rem;
    text-align: center;

    transition: 0.2s all ease;
}

.card_label:hover {
    background-color: #4d476e;
    border: 4px solid #7f92a0;
}

.card_custom-checkbox {
    position: absolute;
    z-index: -1;
    opacity: 0;
}

.selected {
    background-color: #e0f0ea;
    border: 4px solid #7f92a0;
}

.unselected {
    opacity: 0.5;
    background-color: #999999;
    color: #555555;
    border: 4px solid #777777;
}

.correct {
    background-color: #B4E197;
    border: 4px solid #83BD75;
    color: #4E944F;
}

.incorrect {
    background-color: #ff5252;
    border: 4px solid #ff0000;
    color: #a70000;
}
</style>