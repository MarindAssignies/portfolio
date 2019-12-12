<template>
    <div class="about">
        <div class="intro translate-in">
            <div class="container">
                <h2>Hey you !</h2>
                <p class="line-before blue intro-title">How do you do ? 🤝</p>
                <p>
                    My name is
                    <span class="name" @mouseover="imgVisible = true" @mouseleave="imgVisible = false">Marin
                        d'Assignies</span>, I study digital marketing, web development & design at HETIC, in Paris.
                </p>
                <p>I'm soooo in love with ocean and sailing ⛵</p>
                <p> I feel the same freedom when I'm on a boat as in the digital world, we create our own journey. I
                    also love team sports, that's why I love working in team, especially with friendly people. I love to
                    travel and discover more, I'm always looking for new challenges !
                </p>
                <p>Oh one last thing, I can't live without tea ☕</p>
            </div>
        </div>
        <div class="experiences translate-in">
            <div class="container">
                <h2>Experiences</h2>
                <Experience v-for="_experience in experiences" :key="_experience.id" :dates="_experience.dates"
                    :title="_experience.title" :description="_experience.description" />
            </div>
        </div>
        <div class="freelance translate-in">
            <div class="container">
                <h2>Yes, we can (work together)</h2>
                <p class="line-before blue intro-title">Hire me 👔</p>
                <p>
                    Thanks to the notions learned during my last three years at HETIC with professional speakers, I am
                    able to help you to carry out your projects. If you're looking for someone to help you grow your
                    business, manage part of your projects or improve your marketing strategy, I'm the one !
                </p>
                <p>Please feel free to contact me if I can help you on your projects. 😊</p>
                <p class="credit">
                    By the way, this portfolio was designed by
                    <a href="https://hugochapelain.fr" target="_blank">Hugo 🔥</a> and animated by
                    <a href="https://alphonsebouy.fr" target="_blank">Alphonse ✨</a>
                </p>
            </div>
        </div>
        <div class="contact fade-in">
            <h3>
                Let's talk !
                <svg width="27" height="13" viewBox="0 0 27 13" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M25 6.5H1" stroke="#33374F" stroke-width="2" stroke-linecap="square" />
                    <path d="M25.3676 6.71021L19.0288 12" stroke="#33374F" stroke-width="2" />
                    <path d="M25.3676 6.28979L19.0288 0.999986" stroke="#33374F" stroke-width="2" />
                </svg>
            </h3>
            <p class="contact-font">Email</p>
            <p class="link">
                <a href="mailto:mdassignies@gmail.com">mdassignies@gmail.com</a>
            </p>
            <p class="contact-font">LinkedIn</p>
            <p class="link">
                <a href="https://www.linkedin.com/in/marin-d-assignies-77a741153/" target="_blank">Marin d'Assignies</a>
            </p>
            <p class="contact-font">Twitter</p>
            <p class="link">
                <a href="https://twitter.com/digitalsailor_" target="_blank">@digitalsailor_</a>
            </p>
        </div>
        <div :class="{visible: imgVisible}" class="picture">
            <img src="@/assets/img/marin.jpg" alt="It's a picture of me !" />
        </div>
    </div>
</template>

<script>
    import Experience from "@/components/Experience.vue";
    export default {
        name: 'About',
        components: {
            Experience
        },
        data() {
            return {
                imgVisible: false,
                experiences: this.$parent.portfolio_contents.experiences
            }
        },

        methods: {
            animateIn() {
                TweenMax.staggerFrom('.translate-in', 0.9, {
                    yPercent: 100,
                    opacity: 0,
                    ease: Power3.easeOut
                }, 0.1)
                TweenMax.from('.fade-in', 0.9, {
                    opacity: 0,
                    ease: Power3.easeOut
                })
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
        beforeRouteLeave(to, from, next) {
            const tl = new TimelineMax({
                onComplete: () => {
                    next()
                }
            })
            tl
                .staggerTo('.translate-in', 0.9, {
                    yPercent: 100,
                    opacity: 0,
                    ease: Power3.easeOut
                }, 0.1)
                .to('.fade-in', 0.9, {
                    opacity: 0,
                    ease: Power3.easeOut
                }, "-=0.9")
        }

    }
</script>

<style lang="scss" scoped>
    .about {
        position: relative;
    }

    .contact,
    .picture {
        position: fixed;
        right: 0;
        top: 17vh;
        width: 350px;
        padding: 10rem 0;

        h3 {
            margin-top: 0;
        }

        @media screen and (max-width: 800px) {
            position: static;
            padding-left: 10rem;
        }

        @media screen and (max-width: 800px) {
            padding-left: 1rem;
        }
    }

    .picture {
        top: 5vh;
        height: 800px;
        display: none;

        @media screen and (max-width: 800px) {
            position: absolute;
        }

        &.visible {
            display: block;
        }
    }

    .picture img {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    h2 {
        font-family: var(--title-font);
        font-size: 3rem;
        margin-top: 0;
    }

    .intro {
        width: 55%;

        @media screen and (max-width: 800px) {
            width: 100%;
        }
    }

    .intro-title {
        text-transform: uppercase;
        color: var(--light-blue);
        font-weight: bold;
    }

    .name {
        color: var(--light-blue);
        position: relative;

        &::after {
            content: "";
            position: absolute;
            left: 0;
            top: calc(100% + 1px);
            width: 100%;
            height: 1px;
            background-color: var(--light-blue);
        }
    }

    .experiences {
        background-color: white;
    }

    .intro,
    .experiences,
    .freelance {
        padding: 3rem 0;
    }

    .freelance {
        width: 55%;

        @media screen and (max-width: 800px) {
            width: 100%;
        }
    }

    .credit {
        font-size: 0.9rem;
        margin-top: 5rem;
    }

    .contact-font {
        font-family: var(--title-font);
        margin-bottom: 0.5rem;
    }

    a {
        text-decoration: none;
        color: var(--light-blue);
    }

    .link {
        margin-bottom: 1rem;
    }
</style>