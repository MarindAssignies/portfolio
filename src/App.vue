<template>
  <div id="app">
    <Header/>
    <router-view/>
    <Footer/>
  </div>
</template>

<script>
import * as GSAP from 'gsap'

import Header from "@/components/Header.vue"
import Footer from "@/components/Footer.vue"

import PortfolioContents from "@/assets/portfolio-contents.json"

//assets are all images present on the homepage
const assets = [
  'thumbnail-idalgo.png',
  'thumbnail-warpcoreaudio.jpg',
  'thumbnail-alphacomposite.jpg',
  'thumbnail-sohetic.png',
  'project-idalgo.jpg',
  'project-warpcoreaudio.png',
  'project-alphacomposite.jpg',
  'project-sohetic.png'
]

let loadedAssets = 0
let assetErrors = 0

export default{
  components: {
    Header,
    Footer
  },

  data () {
    return {
      portfolio_contents: PortfolioContents
    }
  },

  mounted () {
    this.loadAssets();
  },

  methods: {
    loadAssets () {
      const $counter = document.querySelector('.js-loader-counter')
      const counter = { value: 0 }
      for (const _asset of assets) {
        const image = new Image()
        image.addEventListener('load', () => {
          loadedAssets++
          TweenMax.to(counter, 1, {
            value: Math.floor((loadedAssets + assetErrors) / assets.length * 100),
            onUpdate: () => {
              $counter.textContent = Math.floor(counter.value)
            },
            onComplete: () => {
              if ((loadedAssets + assetErrors) === assets.length) {
                TweenMax.delayedCall(1, 
                  () => {
                    const $loader = document.querySelector('.loader')
                    const $counter = document.querySelector('.js-loader')

                    window.appLoaded = true
                    const event = new CustomEvent('app::loaded')

                    const tl = new TimelineMax({ onComplete: () => {
                      window.dispatchEvent(event)
                    }})
                      .to($counter, 0.5, {
                        y: 100,
                        autoAlpha: 0
                      })
                      .set($loader, {
                        autoAlpha: 0
                      })
                  }
                )
              }
            }
          })
        })
        image.addEventListener('error', () => {
          assetErrors++
          console.error(`Could not load asset ${ _asset }`)
        })
        image.src = require(`./assets/img/${ _asset }`)
      }
    }
  }
}

</script>


<style lang="scss">
  :root{
    --main-font:'Work Sans', sans-serif;
    --title-font:'Playfair Display', serif;
    --dark-blue: #33374F;
    --light-blue: #4354C8;
    --main-bg-color: #fffbf2;
  }
  
  ::-webkit-scrollbar {
    width: 0;
  }

  *,
  *::before,
  *::after{
    box-sizing: border-box;
  }

  body{
    margin: 0;
    font-family: var(--main-font);
    background-color: var(--main-bg-color);
    overflow-x: hidden;
    p{
      margin-top: 0;
    }
  }

  .line-before{
    position: relative;
    padding-left: 25px;
    &::before{
      content: '';
      width: 20px;
      height: 1px;
      background-color:#33374F;
      position: absolute;
      left: 0;
      top: 50%;
      transform: translateY(-50%);
    }
    &.blue::before{
      background-color:#4354C8;
    }
  }
  
  a>p.line-before{
    &::before{
      transition: width .3s cubic-bezier(0.47, 0, 0.745, 0.715);
    }
    &:hover{
      &::before{
        width: 100%;
      }
    }
  }
  

  .container{
    padding: 0 10rem;
    @media screen and (max-width: 800px) {
      padding: 0 1rem;
    }
  }


  
</style>
