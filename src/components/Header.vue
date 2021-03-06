<template>
    <div class="header">
        <h1 class="title">{{title}}</h1>
    </div> 
</template>

<script>
export default {
    name: "Header",
    props: {
        title: String
    }
}
</script>

<style scoped>
.header {
    margin: auto;
    height: 100px;
    width: 700px;
    border: 1px solid white;
    display: flex;
    justify-content: center;
    align-items: center;
}

.title {
    color: white;
}
</style>