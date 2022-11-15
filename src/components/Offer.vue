<template>
    <div>
        <h2 v-if="offer">Your offer</h2>
        <p>{{ offer }}</p>
    </div>

</template>

<script>
export default {
    props: ['offer'],
}


</script>