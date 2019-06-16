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
          <router-link v-for="(_project, index) in projects" :key="_project.id" :to="`/projects/${_project.slug}`">
            <p @mouseleave="_event => handleTitleLeave(_event)" @mouseover="_event => handleTitleHover(index, _project.thumbnail, _project.slug, _event)" :class="{'focused': index === focusedIndex }">{{ _project.title }}</p>
          </router-link>
        </div>
      </div>
    </div>
    <router-link :to="`projects/${project_slug}`">
      <div class="project-img-container">
        <img ref="projectImg" class="project-img" :src="require(`@/assets/img/${thumbnail_src}`)" alt="project-img">
      </div>
    </router-link>
  </div>
</template>

<script>
import { clearInterval } from 'timers';
// @ is an alias to /src

export default {
  name: 'home',
  data () {
    return {
      projects: this.$parent.portfolio_contents.projects,
      thumbnail_src: '',
      project_slug: '',
      focusedIndex: 0,
      interval: null
    }
  },
  methods: {
    handleTitleHover(_index, _thumbnail, _slug, _event){
      this.thumbnail_src = _thumbnail
      this.project_slug = _slug
      window.clearInterval(this.interval)
      this.focusedIndex = _index
      _event.target.style.transform = 'translateX(15px)'
      this.$refs.projectImg.parentNode.style.width = '300px';
    },
    handleTitleLeave(_event){
      this.launchInterval()
      _event.target.style.transform = 'translateX(0)'
      this.$refs.projectImg.parentNode.style.width = '250px'
    },
    launchInterval(){
      this.interval = window.setInterval(() => {
        this.$refs.projectImg.style.opacity = 0
        setTimeout(() => {
          ++this.focusedIndex > (this.projects.length - 1) ? this.focusedIndex = 0 : null
          this.project_slug = this.projects[this.focusedIndex].slug
          this.thumbnail_src = this.projects[this.focusedIndex].thumbnail
          this.$refs.projectImg.addEventListener('load', ()=>{
            this.$refs.projectImg.style.opacity = 1
          })
        }, 800);
      }, 7000); 
    }
  },
  beforeMount () {
    this.thumbnail_src = this.projects[0].thumbnail
    if (window.width > 800) {
      this.project_slug = this.projects[0].slug
    }
  },
  mounted() {
    if (window.width > 800) {
      this.launchInterval()
    }
  },

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
  svg{
    transition: transform 0.3s cubic-bezier(0.47, 0, 0.745, 0.715);
  }
  &:hover svg{
    transform: translateX(15px);
  }

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
  transition: transform .3s;
}

a {
  text-decoration: none;
  color: var(--dark-blue);
}

.projects p:hover, .projects p.focused {
  color: var(--light-blue);
}

@media screen and (max-width: 800px){
  .projects p.focused{
    color: var(--dark-blue);
  }
}

.flex-container{
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.project-img-container{
  position: absolute;
  width: 250px;
  height: 70%;
  top: 50%;
  right: 0;
  transform: translateY(-50%);
  overflow: hidden;
  transform-origin: right;
  transition: width .4s;
}

.project-img{
  position: absolute;
  top: 0;
  right: -50px;
  width: 350px;
  height: 100%;
  display: block;
  object-fit: cover;
  transition: opacity .7s;
  @media screen and (max-width: 800px){
     display: none;
    }
}
</style>
