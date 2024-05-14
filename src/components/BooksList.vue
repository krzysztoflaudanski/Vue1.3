<template>
<div>
  <ul>
    <li :key="index" v-for="(book, index) in books">
      {{ book.title }}, {{ book.price }}
      <button @click="removeBook(index)">Remove</button>
    </li>
  </ul>
</div>
</template>

<script>
export default {
  name: 'BooksList',
  props: {
    books: {
      type: Array,
      required: true
    },
    removeBook: {
      type: Function,
      required: true
    }
  }
}
</script>
