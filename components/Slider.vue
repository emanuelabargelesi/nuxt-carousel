<template>
  <transition name="fade">
    <div class="carousel-slider w-screen mx-auto" v-if="show" :style="style">
      <VueSlickCarousel :arrows="true" :dots="true" v-bind="settings">
        <template v-for="post in posts">
          <div @mouseover="isHovering = true" @mouseout="isHovering = false">
            <img class="mx-auto rounded-3xl object-fill" :src="post.image" :alt="post.content"
                 :class="{'filter brightness-50': isHovering}">
            <div
              class="card-slider opacity-0 bg-transparent absolute inset-0 flex flex-col justify-center h-full mx-auto md:p-10 sm:p-5 md:text-base sm:text-xs text-white"
              :class="{'opacity-100': isHovering}">
              <p class="text-2xl" v-text="post.title + ' - ' + post.continent"></p>
              <p class="mt-3" v-text="post.description"></p>
            </div>
          </div>
        </template>
      </VueSlickCarousel>
    </div>
  </transition>
</template>

<script>

import VueSlickCarousel from 'vue-slick-carousel'
import 'vue-slick-carousel/dist/vue-slick-carousel.css'
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css'

export default {
  components: {VueSlickCarousel},

  data() {
    return {
      show: false,
      response: [],
      riverLength: "",
      settings: {
        "dots": true,
        "arrows": true,
        "initialSlide": 0,
        "autoplay": false,
        "adaptiveHeight": false,
        "focusOnSelect": false,
        "draggable": true,
        "fade": true
      },
      isHovering: false,
      arrows: "#000000",
      dots: "#d3d8f2"
    }
  },

  mounted() {
    $nuxt.$on("show-slider", (posts, show) => {
      this.response = posts;
      this.show = show;
    });

    $nuxt.$on("dark-theme", this.changeDark);
    $nuxt.$on("light-theme", this.changeLight);
  },

  methods: {
    changeDark() {
      this.arrows = "#d3d8f2";
      this.dots = "#1f2a37";
    },
    changeLight() {
      this.arrows = "#000000";
      this.dots = "#d3d8f2";
    }
  },

  computed: {
    posts() {
      return this.response.filter(post => !post.length.indexOf(this.riverLength))
    },
    style() {
      return {
        "--arrows": this.arrows,
        "--dots": this.dots
      }
    }
  }
}
</script>

<style lang="scss">
.carousel-slider {
  img {
    width: 90vw;
    height: 400px;
    cursor: pointer;

    @media only screen and (min-width: 1024px) {
      width: 60vw;
    }
  }
}

.slick-slider {
  .card-slider {
    width: 90vw;
    transition: .5s ease;

    @media only screen and (min-width: 1024px) {
      width: 60vw;
    }
  }
}

.slick-prev:before,
.slick-next:before {
  color: var(--arrows);
}

.slick-next {
  display: none !important;
  @media only screen and (min-width: 600px) {
    display: block !important;
    right: 1rem;
  }
  @media only screen and (min-width: 1024px) {
    display: block !important;
    right: 10rem;
  }
  @media only screen and (min-width: 1400px) {
    display: block !important;
    right: 17rem;
  }
}

.slick-prev {
  display: none !important;
  @media only screen and (min-width: 600px) {
    display: block !important;
    left: 1rem;
  }
  @media only screen and (min-width: 1024px) {
    display: block !important;
    left: 10rem;
  }
  @media only screen and (min-width: 1400px) {
    display: block !important;
    left: 17rem;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 2.5s;
}

.fade-enter,
.fade-leave-active {
  opacity: 0;
}

.slick-dots:not(#_) {
  background-color: var(--arrows);
  margin-top: 2rem;
  display: flex !important;
  left: 50%;
  transform: translateX(-50%);
  border-radius: 1rem;
  width: auto;
  padding: .25rem;

  button:before {
    color: var(--dots);
    opacity: 1;
  }

  .slick-active button:before {
    color: #33B8FF;
  }
}

</style>
