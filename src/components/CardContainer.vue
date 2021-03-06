<template>
    <div v-if="cardArray.length" class="card-container">
        <div v-for="(card, index) in cardArray" :key="index">
            <Card v-on="$listeners" :card="card.name" :isShown="card.isShown" :id="index"/>
        </div>
    </div>
    <div v-else class="info-container">
        <h2 class="sub-title">Welcome to Card Match</h2>
        <p class="how-to-play">
            OBJECTIVE:<br> 
            Begin by clicking one card after another.<br>
            MATCH:<br> 
            "Matched" score increases by one.<br> 
            Both cards remain face up<br> 
            NO MATCH:<br> 
            Both cards flip face donw<br>
            WIN:<br>  
            All cards face up.
        </p>
        <h2 class="sub-title" @click="handleClick">Click New Game To Begin</h2>
    </div>
</template>

<script>
import Card from './Card';

export default {
    components: {
        Card
    },
    name: "CardContainer",
    props: {
        cardArray: Array
    },
    methods: {
        handleClick() {
            this.$emit("clickNewGame");
        }
    }
}
</script>

<style scoped>
* {
    --var-container-width: 700px;
}

.card-container {
    margin: auto;
    height: 500px;
    width: var(--var-container-width);
    border: 1px solid white;
    display: grid;
    justify-items: center;
    align-items: center;
    grid-template-columns: repeat(6, auto)
}

.info-container {
    margin: auto;
    height: 500px;
    width: 700px;
    border: 1px solid white;
}

.sub-title {
    color: white;
    text-align: center;
    padding-top: 25px;
    cursor: pointer;
}

.how-to-play {
    color: white;
    margin: auto;
    width: calc(var(--var-container-width) * .5);
    text-align: center;
    padding-top: 25px;
}

</style>