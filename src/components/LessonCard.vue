<template>
  <div>
    <div class="border p-4 bg-white">
      <div class="d-flex justify-content-between">
        <div>
          <h3>{{ lesson.subject }}</h3>
          <p p>Location: {{ lesson.location }}</p>
          <p>Price: ${{ lesson.price }}</p>
          <p>
            <b>Spaces: {{ lesson.spaces }}</b>
          </p>
        </div>

        <img
          :src="getImageUrl(lesson.image)"
          alt="lesson.image"
          class="img-fluid"
          style="width: 90px; height: 100%"
        />
      </div>
      <button
        class="btn btn-lg btn-success col-12 col-md-8 mx-auto"
        @click="addToCart"
        :disabled="lesson.spaces <= 0"
      >
        {{ lesson.spaces > 0 ? 'Add to Cart' : 'Sold Out' }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    lesson: Object,
  },
  methods: {
    addToCart() {
      if (this.lesson.spaces > 0) {
        this.$emit('add-to-cart', this.lesson)
      }
    },

    getImageUrl(imagePath) {
      const baseUrl =
        process.env.NODE_ENV === 'production' ? '/kamal_store_frontend/' : '' // Development URL
      console.log(`baseURL: ${baseUrl}${imagePath}`)
      return `${baseUrl}${imagePath}` // e.g., images/guitar-icon.jpg
    },
  },
}
</script>
