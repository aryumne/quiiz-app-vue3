<template>
    <h2 width="100%" class="bg-pink py-3">QUIZ APP</h2>
    <h3 class="py-4">Congratulation Your Score is</h3>
    <h1 class="py-1">{{ score }}</h1>
</template>

<script>
export default {
    name: "Congratulation",
    props: ["score"]
}
</script>
<style scoped>
h1 {
    font-size: 5rem;
}
</style>