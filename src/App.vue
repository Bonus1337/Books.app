<template>
  <div id="app" class="app">
    <!-- heading -->
    <header class="app__heading">
      <h1>Books<span>.app</span></h1>
    </header>

    <!-- books list -->
    <BooksList
    :books="books"
    @remove="removeBook" />

    <!-- no books message -->
    <BooksLengthMsg :books="books" />

    <!-- add book form -->
    <BookForm @add="addBook" />
    <BooksSummary :books="books" />
  </div>
</template>
<script>
import BooksList from './components/BooksList'
import BooksLengthMsg from './components/BooksLengthMsg'
import BookForm from './components/BookForm'
import BooksSummary from './components/BooksSummary'
import axios from 'axios'
export default {
  name: 'App',
  components: {
    BooksList,
    BooksLengthMsg,
    BookForm,
    BooksSummary
  },
  data: () => ({
    books: []
  }),
  methods: {
    removeBook (index) {
      this.books.splice(index, 1)
    },
    addBook (book) {
      this.books.push({ ...book })
    }
  },
  created () {
    axios.get('https://api.itbook.store/1.0/new')
      .then(response => {
        this.books = response.data.books
        while (this.books.length > 2) {
          this.books.pop()
        }
      })
      .catch(error => {
        console.log(error)
      })
  }
}
</script>
<style lang="scss" scoped>
.app {
  width: 100%;
  max-width: 1000px;
  padding: 2rem;
  margin: 0 auto;

  &__heading {
    font-size: 3rem;
    text-align: center;
    span {
      color: #5a58da;
    }
  }
}
</style>
