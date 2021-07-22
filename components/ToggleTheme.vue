<template>
  <div class="flex justify-end items-center space-x-2 mx-10 -mt-40">
    <span class="text-sm text-gray-700">Light</span>
    <div>
      <input type="checkbox" id="toggle" class="hidden">
      <label for="toggle" @click="toggle">
        <div class="w-9 h5 flex items-center bg-gray-300 rounded-full p-1">
          <div class="toggle-button w-4 h-4 bg-white rounded-full shadow-md transform duration-300 ease-in-out"></div>
        </div>
      </label>
    </div>
    <span class="text-sm text-gray-400">Dark</span>
  </div>
</template>

<script>

export default {
  methods: {
    toggle() {
      const checkbox = document.querySelector("#toggle");
      const darkDiv = document.querySelector(".slider-container");
      if (!checkbox.checked) {
        darkDiv.classList.add("dark");
        $nuxt.$emit("dark-theme");
      } else {
        darkDiv.classList.remove("dark");
        $nuxt.$emit("light-theme");
      }
    }
  },
  beforeDestroy() {
    $nuxt.$off('dark-theme');
    $nuxt.$off('light-theme');
  }
}

</script>
