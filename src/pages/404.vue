<template>
  <layout v-if="!isRedirect">

    <MetaInfo
      :pageTitle = "'Page not found'"
      :pageDescription = "'In some reason the page you were looking for was not found (maybe it was deprecated or url has a typo). Anyway, you may use navigation on robonomics.network to find what you need.'"
    />

    <section class="section__solid section__404">
      <div class="layout layout__content">
        <h1 v-if="$ts('404_title')">{{$ts('404_title')}}</h1>
      </div>

      <!-- <div class="layout hyphens layout__text_small">
        <p>{{ $ts('404string_1') }}:</p>
        <ul>
          <li>{{ $ts('404reason_1') }};</li>
          <li>{{ $ts('404reason_2') }};</li>
          <li>{{ $ts('404reason_3') }}.</li>
        </ul>

        <p>
          <b>{{ $ts('This page may need translation') }}.</b>
          <br/>
          {{ $ts('If you want to help us with translation') }}:
        </p>
        <ul>
          <li>{{ $ts('contact us at') }}: <a href="mailto:localization@robonomics.network?subject=Robonomics%20WIKI%20Localization">localization@robonomics.network</a></li>
          <li>{{ $ts('or') }} {{ $ts('send') }} <g-link to="https://github.com/airalab/robonomics.network">GitHub PR</g-link></li>
        </ul>
      </div> -->
      <p >
        Check url once more or create an <g-link class="link" to="https://github.com/airalab/robonomics.network/issues">issue</g-link> telling us that you’ve got 404 error (do not forget to mention current url)
      </p>

      <div  class="page-404__bg" aria-hidden="true">
        <div id="parallax" class="parallax-objects">
          <div data-depth="0.9" class="page-404__bg-flying parallax-layer">
            <g-image id="parallax-flying" src="~/assets/images/page-404-flying.png"/>
          </div>
          <div class="parallax-layer page-404__bg-asteroids" data-depth="0.9">
            <g-image id="parallax-asteroids" src="~/assets/images/page-404-asteroids.png"/>
          </div>
          <div  data-depth="0.8" class="page-404__bg-bread-1 parallax-layer">
            <g-image id="parallax-bread-1" src="~/assets/images/page-404-bread-1.png"/>
          </div>
          <div  data-depth="0.7" class="page-404__bg-bread-2 parallax-layer">
            <g-image id="parallax-bread-2" src="~/assets/images/page-404-bread-2.png"/>
          </div>
        </div>
        <div class="page-404__big-bg">
          <g-image src="~/assets/images/page-404-img.png"/>
        </div>
      </div>
    </section>


  </layout>
</template>


<script>
  import Navigation from '~/components/Navigation.vue'
  import MetaInfo from '~/components/MetaInfo.vue'
  import Parallax from 'parallax-js'

  export default {

    components: {
      Navigation,
      MetaInfo
    },

    data() {
      return {
        isRedirect: true,
      }
    },

    mounted() {
      const scene = document.getElementById('parallax');
      const parallaxInstance = new Parallax(scene);
    },

    created() {
      // redirect for posts that does not have translations yet
      const path = this.$route.path; 
      const title = path.match(/\/([^\/]+)[\/]?$/);

      if(path.includes(`blog/${this.$locale}`) && !path.includes('tag')) {
        
        window.location.href = `/blog-translations/${title[1]}/`;
      } else {
        this.isRedirect = false
      }
    }

  }
</script>

<style scoped>
  .section__404 {
    height: 100%;
    padding-bottom: 0;
    padding-left: var(--space);
    padding-right: var(--space);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    font-weight: 600;
    background-color: #000;
    color: #fff;
    overflow: hidden;
  }

  .section__404 h1 {
    margin-top: 0;
    padding-top: 0;
    color: var(--color-link-contacts);
    text-shadow: -5px 2px #fff;
  }

  .section__404 p {
    max-width: 625px;
    width: 100%;
    text-align: center;
  }

  .link {
    text-decoration: none;
    color: var(--color-link-contacts);
  }

  #parallax {
    width: 606px;
    margin: 0 auto;
    z-index: 10;
  }

  .page-404__bg img {
    display: inline-block;
    width: 100%;
    filter: contrast(1.5);
  }

  .page-404__big-bg img {
    min-height: 500px;
    height: 100%;
    object-fit: cover;
  }

  .parallax-layer img{
    position: absolute;
  }

  .parallax-layer {
    position: absolute;
    width: 100%;
    height: 100%;
  }

  #parallax-flying {
    left: calc(10% + 636px);
    top: calc(15% + 50px);
    width: 134px;
    /* animation: xAxis 4.5s infinite ease-in-out, yAxis 4.5s infinite ease-out; */
  }

  #parallax-asteroids {
    right: calc(-7% + 27px);
    top: calc(15% + 219px);
    width: 154px;
  }

  #parallax-bread-1 {
    left: calc(100% + 49px);
    bottom: -472px;
    width: 55px;
  }

  #parallax-bread-2 {
    left: calc(10% - 140px);
    top: calc(15% + 364px);
    width: 94px;
  }

  @keyframes yAxis {
    50% {
      transform: translateY(-100px) rotate(90deg);
    }
  }

  @keyframes xAxis {
    50% {
      transform: translateX(100px) rotate(-45deg);
    }
  }

  @media screen and (max-width: 1240px) {
    #parallax-flying {
      left: calc(10% + 332px);
      top: calc(15% + 4px);
    }

    #parallax-asteroids {
      right: calc(4% + 43px);
      top: calc(15% + 153px);
      width: 132px;
    }

    #parallax-bread-1 {
      left: calc(100% - 107px);
      bottom: -383px;
    }

    #parallax-bread-2 {
      left: calc(10% - 122px);
      top: calc(15% + 364px);
    }
  }

  @media screen and (max-width: 935px) {

    #parallax-flying {
      left: calc(10% + 151px);
    }
    
    #parallax-bread-2 {
      left: calc(10% - 77px);
      top: calc(15% + 323px);
    }

  }

</style>