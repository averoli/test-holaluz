<template>
    <article v-if="client">
        <hgroup>
            <h2>{{ client.full_name }}</h2>
            <p>{{ client.address }}</p>
            <p>{{ client.cups }}</p>
            <p>{{ client.role }}</p>
            <p>{{ client.building_type }}</p>
        </hgroup>
    </article>
    <Offer :client="client" />
</template>

<script>
import Offer from './Offer.vue';
export default {
    props: ['client'],
    components: { Offer }
}
</script>