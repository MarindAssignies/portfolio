<template>
    <div class="description">
        <h3>{{ title }}</h3>
        <p>{{ paragraph }}</p>
    </div>
</template>

<script>

export default {
    name: 'Description',
    props: {
        title: String,
        paragraph: String
    }
}
</script>

<style lang="scss" scoped>

.description{
    width: 55%;
    margin: 0 auto;
    margin-bottom: 4rem;
    @media screen and (max-width: 600px){
        width: 100%;
    }
}

h3{
    color: var(--light-blue);
    font-family: var(--title-font);
    font-size: 2rem;
    margin-bottom: 1.5rem;
}

p{
    color: var(--dark-blue);
}
</style>
