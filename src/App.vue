<template>
<div id="app" class="app">

  <!-- heading -->
  <header class="app__heading">
    <h1>Books<span>.app</span></h1>
  </header>

  <!-- books list -->
  <books-list :books="books" :removeBook="removeBook" />

  <!-- no books message -->
  <books-length-msg :books="books.length" />

  <!-- add book form -->
  <book-form @add="addBook" />

  <books-summary :summary="booksSum" />

</div>
</template>

<script>
import BooksList from './components/BooksList'
import BooksLengthMsg from './components/BooksLengthMsg'
import BookForm from './components/BookForm'
import BooksSummary from './components/BooksSummary'

export default {
  name: 'App',
  data: () => ({
    books: [
      {
        title: 'The Catcher in the Rye',
        price: 20
      },
      {
        title: 'Of Mice and Men',
        price: 18
      }
    ]
  }),
  methods: {
    // eslint-disable-next-line
    removeBook(index) {
      this.books.splice(index, 1)
    },
    // eslint-disable-next-line
    addBook(book) {
      this.books.push({ ...book })
    }
  },
  computed: {
    // eslint-disable-next-line
    booksSum() {
      const totalPrice = this.books.reduce((total, book) => total + book.price, 0)
      const totalBooks = this.books.length
      return { totalPrice, totalBooks }
    }
  },
  components: {
    BooksList,
    BooksLengthMsg,
    BookForm,
    BooksSummary
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
