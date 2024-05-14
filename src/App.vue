<template>
<div id="app">

  <!-- heading -->
  <header>
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
