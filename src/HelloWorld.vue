<!-- view -->
<template>

    <h1>Speed Typer</h1>
    <p>
        <span :class="{correct: keyword.correct, wrong: keyword.wrong, pending: keyword.pending}"
        :key="keyword.text" v-for="keyword in keywords">{{keyword.text}} {{''}}</span>
    </p>
    <input type="text" :value="inputValue" @keyup.enter="processInput($event)" />
</template>

<!-- logic -->
<script>
const defaultKeywords = [
   "firm",
    "loyal",
    "truehearted",
    "tight",
    "immobile",
    "flying",
    "quick",
    "fasting",
    "debauched",
    "degenerate",
    "degraded",
    "dissipated",
    "dissolute",
    "libertine",
    "profligate",
    "riotous"
].map(keyword => {
    return{
        text:keyword,
        correct:false,
        wrong:false,
        pending:true,

    };
});

export default {
    data (){
        return {
            inputValue: "",
            index:0,
            keywords: defaultKeywords,
        };
    },
    methods:{
        processInput(event){
            // console.log(event);
            const value = event.target.value.trim();

            if (value === ""){
                return;
            }

            if (this.keywords[this.index].text === value){
                //correct answer
                this.keywords[this.index].correct = true
                this.keywords[this.index].wrong = false
                this.keywords[this.index].pending = false
            }else{
                //wrong answer
                 this.keywords[this.index].correct = false
                this.keywords[this.index].wrong = true
                this.keywords[this.index].pending = false
            }
            this.inputValue = "";
            this.index++;
        },
    },
};
</script>

<!-- style -->
<style scoped>
.pending {
    font-weight: bold;
}

.correct {
    font-weight: bold;
    color: green;
}

.wrong {
    font-weight: bold;
    color: red;
}
</style>