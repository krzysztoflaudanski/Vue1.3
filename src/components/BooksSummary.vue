<script>
export default {
    name: 'BooksSummary',
    props: {
        summary: {
            type: Object,
            required: true
        }
    }
}
</script>

<template>
<p>Books amount: {{ summary.totalBooks }}</p>
<p>Books price: {{ summary.totalPrice }}</p>
</template>
