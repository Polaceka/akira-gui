<template>
    <div v-if="event">
        <h1>{{ event.name }}</h1>
        <p>Event ID: {{ id }}</p>
        <p>Description{{ event.description }}</p>
        <p>Track: {{ event.trackname }}</p>
        <div v-for='group in event.group' :key="group.id" class="group">
            <h2>{{ group.name }}</h2>
            <div v-for='journey in group.journeytime' :key="journey.id">
                <p>Start: {{ journey.start }}</p>
                <p>End: {{ journey.start }}</p>
                <br>
            </div>
        </div>

    </div>
    <div v-else>
        <h1>Loading ...</h1>
    </div>
</template>

<script>
export default {
    props: ['id'],
    data() {
        return {
            event: null
        }
    },
    mounted() {
        fetch('http://localhost:3000/v1/event/' + this.id)
            .then(res => res.json())
            .then(data => this.event = data.event)
            .catch(err => consol.log(err.message))
    }
}
</script>

<style>
    .group{
        background: #f4f4f4;
        padding: 10px;
        border-radius: 3px;
        margin: 10px auto;
        max-width: 500px;
        cursor: pointer;
        color: #444;
    }
</style>