<template>
    <div 
        class="card"
        :class="!isShown && disableClick"
        :id="id"
        @click="handlClick($event)"
    >
        <div v-if="isShown">
        {{ card }}
        </div>
        <div v-else>I</div>
    </div> 
</template>

<script>
export default {
    name: "Card",
    props: {
        card: Number,
        isShown: Boolean,
        id: Number
    },
    methods: {
        handlClick: function(event) {
            this.$emit("clickCard", event);
        }
    }
}
</script>

<style scoped>
* {
    --var-card-height: 100px;
}

.card {
    color: white;
    font-size: calc(var(--var-card-height) * .5);
    height: var(--var-card-height);
    width: var(--var-card-height);
    border: 1px solid white;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
}

.disableClick {
    pointer-events: none;
}
</style>