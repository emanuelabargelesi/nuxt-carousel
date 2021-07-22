<template>
  <div class="text-center -mt-40" v-if="show">
    <h1 class="text-5xl pb-10 dark:text-gray-200">River Slider</h1>
    <p class="text-center mb-5 dark:text-gray-200">HOW TO: Desktop: mouseover/mouse out, Mobile: click</p>
    <button
      class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
      @click="showSlider">
      Discover the rivers
    </button>
  </div>
</template>

<script>
export default {

  data() {
    return {
      show: true,
      response: []
    }
  },

  async fetch() {
    this.response = await fetch("https://api.nuxtjs.dev/rivers").then(res => res.json());
  },

  methods: {
    showSlider() {
      $nuxt.$emit('show-slider', this.response, this.show);
      this.show = !this.show;
    },
  },
  beforeDestroy() {
    $nuxt.$off('show-slider');
  }
}
</script>
