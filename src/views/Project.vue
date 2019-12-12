<template>
    <div class="project">
        <div class="thumbnail">
            <img :src="require(`@/assets/img/${project.project_img}`)" alt="Image">
        </div>
        <div class="container fade-leave">
            <h1 ref="title">{{project.title}}</h1>
            <div class="intro" ref="intro">
                <div>
                    <p class="line-before blue intro-title">👨‍💼 Role</p>
                    <p>{{project.role}}</p>
                </div>
                <div>
                    <p class="line-before blue intro-title">👌 Why I enjoyed it</p>
                    <p>{{project.why}}</p>
                </div>
                <div>
                    <p class="line-before blue intro-title">📆 When</p>
                    <p>{{project.when}}</p>
                </div>
            </div>
        </div>
        <div class="content">
            <div class="container">
                <p class="quote fade-leave">« {{project.quote}} »</p>
                <div class="content-intro-img fade-leave">
                    <img :src="require(`@/assets/img/${project.intro_img}`)" alt="jh,g">
                </div>
                <div class="content-description fade-leave">
                    <Description v-for="_content in project.contents" :key="_content.id" :title="_content.title" :paragraph="_content.paragraph" />
                </div>
                <div class="conclusion">
                    <div class="conclusion-img">
                        <img :src="require(`@/assets/img/${project.conclusion.img}`)" alt="">
                    </div>
                    <div class="conclusion-text">
                        <h3>{{project.conclusion.title}}</h3>
                        <p v-html="project.conclusion.content" />
                    </div>
                </div>
            </div>
        </div>
        <div class="outro fade-leave">
            <div class="container">
                <div class="flex-container">
                    <router-link :to="`/projects/${project.next_project.slug}`">
                        <p>See the next project <svg width="27" height="13" viewBox="0 0 27 13" fill="none"
                                xmlns="http://www.w3.org/2000/svg">
                                <path d="M25 6.5H1" stroke="#33374F" stroke-width="2" stroke-linecap="square" />
                                <path d="M25.3676 6.71021L19.0288 12" stroke="#33374F" stroke-width="2" />
                                <path d="M25.3676 6.28979L19.0288 0.999986" stroke="#33374F" stroke-width="2" />
                            </svg></p>
                    </router-link>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Description from "@/components/Description.vue"
import { ScrollToPlugin } from 'gsap/ScrollToPlugin'

const plugins = [ScrollToPlugin]

export default {
    name: 'Project',
    components: {
        Description,
    },
    data () {
        return {
            project: this.$parent.portfolio_contents.projects.filter(
                _project => _project.slug == this.$route.params.slug
            )[0]
        }
    },
    watch: {
        '$route' (to, from){
            this.project = this.$parent.portfolio_contents.projects.filter(
                    _project => _project.slug == this.$route.params.slug
                )[0]
        }
    },
    beforeMount() {
        // Tweenmax.set(this.$refs.title, { opacity: 0 })
        // Tweenmax.set(this.$refs.intro_part, { opacity: 0 })
    },
    methods: {
        animateIn() {
            const tl = new TimelineMax()
            tl
                .from(this.$refs.title, 0.6, {
                    y: "+=200",
                    opacity: 0,
                    ease: Power3.easeOut
                })
                .staggerFrom(this.$refs.intro.querySelectorAll('div'), 0.6, {
                    y: "+=200",
                    opacity: 0,
                    ease: Power3.easeOut
                }, 0.2, "-=0.3")
        }
    },
    mounted() {
        if (window.appLoaded) {
            this.animateIn()
        } else {
            window.addEventListener('app::loaded', () => {
                this.animateIn()
            })
        }
    },
    beforeDestroy() {
        TweenMax.killAll()
    },
    beforeRouteLeave (to, from, next) {
        if (to.name !== 'project') {
            const tl = new TimelineMax({ onComplete: () => {
                next()
            }})
            tl
                .to('.fade-leave', 0.8, {
                    yPercent: 10,
                    opacity: 0,
                    ease: Power3.easeOut
                })
                .to('.thumbnail', 0.8, {
                    xPercent: -100,
                    opacity: 0,
                    ease: Power3.easeOut
                }, "-=0.4")
            
        }
    },
    updated() {
        const tl = new TimelineMax({ delay: 0.2 })
        tl
            .to('.thumbnail', 0.8, {
                xPercent: 0,
                opacity: 1,
                ease: Power3.easeOut
            })
            .to('.fade-leave', 0.8, {
                yPercent: 0,
                opacity: 1,
                ease: Power3.easeOut
            })
            .fromTo(this.$refs.title, 0.6, {
                y: "+=200",
                opacity: 0
            },
            {
                y: 0,
                opacity: 1,
                ease: Power3.easeOut
            }, "-=0.8")
            .staggerFromTo(this.$refs.intro.querySelectorAll('div'), 0.6, {
                y: "+=200",
                opacity: 0,
            },
            {
                y: 0,
                opacity: 1,
                ease: Power3.easeOut
            }, 0.2, "-=0.3")
    },
    beforeRouteUpdate(to, from, next) {
        const tl = new TimelineMax({ onComplete: () => {
                next()
            }})
        tl
            .to(window, 1, {scrollTo: 0})
            .to('.fade-leave', 0.8, {
                yPercent: 10,
                opacity: 0,
                ease: Power3.easeOut
            })
            .to('.thumbnail', 0.8, {
                xPercent: -100,
                opacity: 0,
                ease: Power3.easeOut
            }, "-=0.4")
    }
}
</script>

<style lang="scss" scoped>

a svg{
    transition: transform 0.3s cubic-bezier(0.47, 0, 0.745, 0.715);
}

a p {
    padding: 5px 0;
    padding-right: 19px;
    display: block;
    position: relative;
    z-index: 10;
    background-color: var(--main-bg-color);
}

a:hover {
    
    svg{
        transform: translateX(15px);
    }
}


.thumbnail{
    width: 100%;
    height: calc(0.7 * 75vh);
    img{
        width: 100%;
        height: 100%;
        object-fit: cover;
        display: block;
    }
}

h1{
    font-family: var(--title-font);
    font-size: 3rem;
    color: var(--dark-blue);
    margin-bottom: 4rem;
}

.intro-title{
    text-transform: uppercase;
    color: var(--light-blue);
    font-weight: bold;
}

.intro{
    display: flex;
    justify-content: space-between;
    padding-bottom: 2rem;
    &>div{
        width: 30%;
    }
    @media screen and (max-width: 800px){
        flex-wrap: wrap;
        &>div{
            width:100%;
            margin-bottom: 1rem;
        }   
    }
}

.content{
    background-color: white;
    padding: 4rem 0;
}

.content-intro-img{
    width: 100%;
    height: 300px;
    margin-bottom: 6rem;
    img{
        width: 100%;
        height: 100%;
        object-fit: cover;
        display: block;
    }
}

.quote{
    margin-bottom: 5rem;
    text-align: center;
    font-size: 1.6rem;
    margin-top: 2rem;
}

.content-description{
    margin-bottom: 7rem;
}

.conclusion{
    display: flex;
    justify-content: flex-end;
    position: relative;
    flex-wrap: wrap;
    @media screen and (max-width: 800px){
        justify-content: center;
    }
}

.conclusion-text {
    width: 60%;

    h3 {
        font-size: 2rem;
        color: var(--light-blue);
        font-family: var(--title-font);
    }

    @media screen and (max-width: 800px){
        width: 100%;
    }
}

.conclusion-img{
    width: 30%;
    height: 400px;
    position: absolute;
    left: 0;
    z-index: 10;
    img{
        width: 100%;
        height: 100%;
        object-fit: cover;
        display: block;
    }
    @media screen and (max-width: 800px){
        width: 100%;
        position: static;
    }
}

.outro{
    background-color: var(--main-bg-color);
    padding-top: 5rem;
    padding-bottom: 6rem;
    position: relative;
    .next-project-thumbnail {
        position: absolute;
        left: 100%;
        top: 0;
        height: 100%;
        width: 100vw;
        object-fit: cover;
        transition: transform 0.2s;
    }
}

.flex-container{
    display: flex;
    justify-content: flex-end;
    a{
        display: block;
        text-decoration: none;
        color: var(--dark-blue);
        text-transform: uppercase;
        font-weight: bold;
    }
}
</style>
