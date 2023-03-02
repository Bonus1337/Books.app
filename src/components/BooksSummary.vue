<template>
  <p>Books amount: {{ books.length }}</p>
  <p>Books price: {{ totalBooksPrice }}</p>
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
  computed: {
    totalBooksPrice () {
      const total = this.books.reduce(
        (acc, book) => acc + parseFloat(book.price.slice(1)),
        0
      )
      return total.toFixed(2)
    }
  }
}
</script>
