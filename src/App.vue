<template>
  <div id="app">
    <Header/>
    <router-view/>
    <Footer/>
  </div>
</template>

<script>
import Header from "@/components/Header.vue"
import Footer from "@/components/Footer.vue"

import PortfolioContents from "@/assets/portfolio-contents.json"

export default{
  components: {
    Header,
    Footer
  },
  data () {
    return {
      portfolio_contents: PortfolioContents
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

  *,
  *::before,
  *::after{
    box-sizing: border-box;
  }

  body{
    margin: 0;
    font-family: var(--main-font);
    background-color: var(--main-bg-color);
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
