<template>
  <div class="home">
    <div class="container">
      <div class="flex-container">
        <div class="intro">
          <h2 class="line-before blue">Hello there</h2>
          <p>I'm Marin, a 21 years old french product owner studying at HETIC in Paris, always focused on work. I feel
            happy
            when my teammates are proud of our creations. 😊</p>
          <p>I'm also working in Freelance, I can help you handle your projects, feel free to contact me !</p>
          <p class="incentive">Take a look at my projects <svg width="27" height="13" viewBox="0 0 27 13" fill="none"
              xmlns="http://www.w3.org/2000/svg">
              <path d="M25 6.5H1" stroke="#33374F" stroke-width="2" stroke-linecap="square" />
              <path d="M25.3676 6.71021L19.0288 12" stroke="#33374F" stroke-width="2" />
              <path d="M25.3676 6.28979L19.0288 0.999986" stroke="#33374F" stroke-width="2" />
            </svg></p>
        </div>
        <div class="projects">
          <router-link v-for="_project in projects" :key="_project.id" :to="`/projects/${_project.slug}`">
            <p @mouseover="thumbnail_src = _project.thumbnail">{{ _project.title }}</p>
          </router-link>
        </div>
      </div>
    </div>
    <img class="project-img" :src="require(`@/assets/img/${thumbnail_src}`)" alt="project-img">
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'home',
  data () {
    return {
      projects: this.$parent.portfolio_contents.projects,
      thumbnail_src: ''
    }
  },
  mounted () {
    this.thumbnail_src = this.projects[0].thumbnail
  }

}
</script>

<style lang="scss"scoped>

.home{
  height: 75vh;
  display: flex;
  align-items: center;
  position: relative;
  @media screen and (max-width: 800px){
     height: auto;
    }
}

.intro {
  width: 30%;
  margin-right: 12rem;
  @media screen and (max-width: 800px){
      width: 100%;
      margin-right: 0;
      margin-bottom: 3rem;
    }
}

h2 {
  text-transform: uppercase;
  font-weight: bold;
  margin-bottom: 1rem;;
  color: var(--light-blue);
  font-size: 1rem;
}

.incentive {
  margin-top: 3rem;
  text-transform: uppercase;
  font-weight: bold;

  @media screen and (max-width: 800px) {
    svg {
      transform: rotate(90deg);
    }
  }
}

.projects {
  width: 35%;
  font-size: 3rem;
  font-family: var(--title-font);
  @media screen and (max-width: 800px){
     width: 100%;
     margin-bottom: 3rem;
    }
}

.projects p{
  margin-bottom: 2rem;
  line-height: 1;
}

a {
  text-decoration: none;
  color: var(--dark-blue);
}

.projects p:hover {
  color: var(--light-blue);
}

.flex-container{
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.project-img{
  position: absolute;
  width: 250px;
  height: 70%;
  object-fit: cover;
  top: 50%;
  right: 0;
  transform: translateY(-50%);
  @media screen and (max-width: 800px){
     display: none;
    }
}
</style>
