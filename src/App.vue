<template>
  <div id="app">

    <!-- heading -->
    <header>
      <h1>Books<span>.app</span></h1>
    </header>

    <!-- books list -->
    <ul>
      <li :key="index" v-for="(book, index) in books">
        {{ book.title }}, {{ book.price }}$
        <button @click="removeBook(index)">Remove</button>
      </li>
    </ul>

    <!-- no books message -->
    <div>

      <p v-if="books.length > 5">books-amount: {{ books.length }} books</p>
      <p v-if="books.length > 1 && books.length <= 5">Not too many of them…</p>
      <p v-if="books.length === 1"> One single book! </p>
      <p v-show="!books.length">Go get some books!</p>
    </div>

    <!-- add book form -->
    <form @submit.prevent="handleSubmit">
      <label>
        Title:
        <input v-model="form.title" type="text" name="title">

      </label>
      <label>
        price:
        <input v-model="form.price" type="number" name="price">

      </label>
      <button @submit.prevent="handleSubmit">Add book</button>
    </form>
  </div>
</template>

<script>
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
    ],
    form: {
      title: '',
      price: 0
    }
  }),
  methods: {
    // eslint-disable-next-line
    removeBook(index) {
      this.books.splice(index, 1)
    },
    // eslint-disable-next-line
    handleSubmit() {
      this.books.push({ ...this.form })
      this.form.title = ''
      this.form.price = 0
    }
  }
}
</script>
