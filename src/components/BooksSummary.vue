<template>
  <p>Books amout: {{ books.length }}</p>
  <p>Books price: {{ totalBooksPrice() }}</p>
</template>

<script>
export default {
  name: 'BooksSummary',
  props: {
    books: {
      type: Array,
      required: true
    }
  },
  methods: {
    totalBooksPrice () {
      return this.books.reduce((total, book) => total + book.price, 0)
    }
  }
}

</script>
