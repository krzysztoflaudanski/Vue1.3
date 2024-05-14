<template>
<div>
    <p v-if="books> 5">books-amount: {{ books}} books</p>
    <p v-if="books > 1 && books <= 5">Not too many of them…</p>
    <p v-if="books === 1"> One single book! </p>
    <p v-if="books === 0">Go get some books!</p>
</div>
{{ console.log(books) }}
</template>

<script>
export default {
    name: 'BooksLengthMsg',
    props: {
        books: {
            type: Number,
            required: true
        }
    }
}
</script>
