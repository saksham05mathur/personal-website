<template>
  <div>
    <!-- main background image -->
    <section class="hero is-fullheight">
      <div class="hero-body columns is-centered is-vcentered headshot">
        <!-- titles and resume button -->
        <aside class="container section column is-narrow">
          <!-- titles -->
          <h1 class="title">{{ title }}</h1>

          <!-- subtitles with vue-typer -->
          <h2 class="subtitle">
            <vue-typer
              :text="[
                'SEO specialist',
                'Produced over ' + allBlog_postss.totalCount + ' tutorials',
                'Tech enthusiast'
              ]"
              :repeat="Infinity"
              :shuffle="false"
              initial-action="typing"
              :pre-type-delay="70"
              :type-delay="70"
              :pre-erase-delay="2000"
              :erase-delay="250"
              erase-style="select-all"
              :erase-on-complete="false"
              caret-animation="blink"
            ></vue-typer>
          </h2>

          <!-- resume button -->
          <a
            rel="noopener"
            href="https://drive.google.com/open?id=1dx8t_IKZKLtfs4I6nIZsQtaW5qJvL22VEaPZ04L0RsE"
            target="_blank"
          >
            <button class="button is-centered">Resume</button>
          </a>
        </aside>
      </div>
    </section>

    <app-portfolio></app-portfolio>
  </div>
</template>

<script>
import Portfolio from '@/components/Portfolio.vue'
import gql from 'graphql-tag'

const articles = gql`
  {
    allBlog_postss {
      totalCount
    }
  }
`

export default {
  data() {
    return {
      title: 'Mark Perez',
      description:
        'Mark Perez is an SEO Specialist and Self-learning enthusiast in technology. Produces content on YouTube.'
    }
  },

  head() {
    return {
      title: 'SEO Specialist',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.description
        },
        {
          hid: 'og:type', // open graph type
          property: 'og:type',
          content: 'website'
        },
        {
          hid: 'apple-mobile-web-app-title', // open graph mobile web app title
          name: 'apple-mobile-web-app-title',
          content: this.title
        },
        {
          hid: 'og:title', // open graph title
          property: 'og:title',
          content: this.title
        },
        {
          hid: 'og:description', // open graph description
          property: 'og:description',
          content: this.description
        },
        {
          hid: 'og:url', // open graph url
          property: 'og:url',
          content: 'https://markperez.dev' + this.$route.fullPath
        },
        {
          hid: 'og:image', // open graph image
          property: 'og:image',
          content:
            'https://d33wubrfki0l68.cloudfront.net/f602ffaa7d56bbd9f27db7a08a0a7068462149e3/143f6/_nuxt/img/f9c805f.png'
        }
      ]
    }
  },

  components: {
    'app-portfolio': Portfolio
  },

  apollo: {
    allBlog_postss: {
      query: articles,
      fetchPolicy: 'cache-and-network'
    }
  }
}
</script>

<style scoped>
button {
  font-size: 20px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #fff;
  background-color: #00c58e;
}

.title {
  font-size: 70px;
  letter-spacing: 12px;
}

.subtitle {
  font-size: 24px;
}

.is-fullheight {
  min-height: calc(100vh - 6rem);
  background-color: #dbdbdb;
  background-image: linear-gradient(to top, #dbdbdb 55%, #fff 100%);
  background-repeat: no-repeat;
  background-size: cover;
}

.headshot {
  min-height: calc(100vh - 6rem);
  background-image: url('~assets/images/marks-headshot.png');
  background-blend-mode: lighten;
  background-repeat: no-repeat;
  background-size: 33%;
  background-position: bottom 12px right 150px;
}

/* specify background image size on certain breakpoint */
@media only screen and (max-width: 1630px) {
  .headshot {
    background-size: 35%;
    background-position: bottom 12px right 250px;
  }
}

@media only screen and (max-width: 1407px) {
  .headshot {
    background-size: 40%;
    background-position: bottom 12px right 200px;
  }
}

@media only screen and (max-width: 1215px) {
  .headshot {
    background-size: 45%;
    background-position: bottom 12px right 100px;
  }
}

/* change image transparency when window is smaller */
@media only screen and (max-width: 1023px) {
  .headshot {
    background-color: rgba(255, 255, 255, 0.65);
    background-size: 60%;
    background-position: bottom 12px right 75px;
  }
}

@media only screen and (max-width: 780px) {
  .headshot {
    background-size: 75%;
    background-position: bottom 12px right 40px;
  }
}

@media only screen and (max-width: 556px) {
  .headshot {
    background-size: 80%;
    background-position: bottom 12px right 50px;
  }
}
</style>
