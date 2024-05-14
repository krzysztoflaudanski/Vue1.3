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
import axios from 'axios';
import BooksList from './components/BooksList';
import BooksLengthMsg from './components/BooksLengthMsg';
import BookForm from './components/BookForm';
import BooksSummary from './components/BooksSummary';

export default {
  name: 'App',
  data() {
    return {
      books: []
    };
  },
  methods: {
    removeBook(index) {
      this.books.splice(index, 1);
    },
    addBook(book) {
      this.books.push({ ...book });
    },
    async fetchBooks() {
      try {
        const response = await axios.get('https://api.itbook.store/1.0/new');
        const booksData = response.data.books.slice(0, 3).map(book => ({
          title: book.title,
          price: parseFloat(book.price.replace('$', '')) || 0
        }));
        this.books = booksData;
      } catch (error) {
        console.error('Error fetching books:', error);
      }
    }
  },
  computed: {
    booksSum() {
      const totalPrice = this.books.reduce((total, book) => total + book.price, 0);
      const totalBooks = this.books.length;
      return { totalPrice, totalBooks };
    }
  },
  components: {
    BooksList,
    BooksLengthMsg,
    BookForm,
    BooksSummary
  },
  created() {
    this.fetchBooks();
  }
};
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
