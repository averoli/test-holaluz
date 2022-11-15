<template>
    <article v-if="offer">
        <h2>Your offer</h2>
        <p>{{ offer }}</p>
    </article>
</template>

<script>
export default {
    props: ['offer'],
}


</script>