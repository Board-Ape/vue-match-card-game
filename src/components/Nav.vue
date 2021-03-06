<template>
    <div class="nav">
        <div class="text-container">
            <h3 class="matched-text">Matched : <span class="matched">{{matched}}</span> of <span class="total">{{total/2}}</span> </h3>
        </div>
        <h2 v-show="winner" class="winner">WINNER!</h2>
        <button class="new-game-button" @click="handleClick">New Game</button>
    </div> 
</template>

<script>
export default {
    name: "Nav",
    props: {
        matched: Number,
        total: Number,
        winner: Boolean
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
    --var-nav-height: 80px;
}

.nav {
    margin: auto;
    height: var(--var-nav-height);
    width: 700px;
    border: 1px solid white;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.matched-text {
    color: white;
    margin-left: 50px;
}

.winner {
    color: green;
}

.new-game-button {
    height: calc(var(--var-nav-height) * .5);
    margin-right: 50px;
    cursor: pointer;
}

.matched {
    color: lightgreen;
}

.total {
    color: red;
}

</style>