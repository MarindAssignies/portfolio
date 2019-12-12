<template>
    <div class="experience">
        <p class="line-before blue intro-title">{{ dates }}</p>
        <p><strong>{{ title }}</strong></p><p> {{description}}</p>
    </div>
</template>

<script>
export default {
    name: 'Experience',
    props:{
        dates: String,
        title: String,
        description: String
    }
}
</script>

<style lang="scss" scoped>

.experience{
    margin-bottom: 2rem;
}
    
  .intro-title{
    text-transform: uppercase;
    color: var(--light-blue);
    font-weight: bold;
  }
</style>


