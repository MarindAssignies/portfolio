<template>
    <header class="container">
        <router-link to="/">
            <p class="line-before">Marin d'Assignies</p>
        </router-link>
        <router-link to="/about">
            <p class="line-before">About me</p>
        </router-link>
    </header>
</template>

<script>
export default {
    name: 'Header',
}
</script>

<style lang="scss" scoped>

header{
    display: flex;
    justify-content: space-between;
    position: relative;
    padding-top: 3rem;
    padding-bottom: 3rem;
    height: 17vh;
    align-items: center;
    &::after{
        content: '';
        width: 100%;
        height: 1px;
        background-color: var(--dark-blue);
        position: absolute;
        top: 100%;
        left: 0;
        opacity: 0.32;
    }
}

p{
    text-transform: uppercase;
    font-weight: bold;
    margin-bottom: 0;
}

a{
    text-decoration: none;
    color: var(--dark-blue);
}

</style>
