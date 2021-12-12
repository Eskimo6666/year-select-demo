<template>
    <div class="index-cell">
        <span class="cell-year">{{ cardData.year }}</span>
        <main>{{ cardData.content }}</main>
    </div>
</template>

<script>
export default {
    name: 'cell',
    props: {
        cardData: {
            year: '',
            content: ''
        }
    }
}
</script>

<style scoped>
.index-cell {
    margin-top: 20px;
}
.cell-year {
    color: blue;
}
main {
    height: 200px;
    display: flex;
    background-color: grey;
    align-items: center;
    justify-content: center;
}
</style>