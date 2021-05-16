<template>
    <h1>Events</h1>
    <p>Total Events: {{ events.length }}</p>
    <div v-if="events.length">
        <div v-for='event in events' :key="event.id" class="event">
            <router-link :to="{ name: 'EventDetails', params: { id: event.id }}">
                <h2>{{ event.name }}</h2>
                <p>{{ event.startdate }}</p>
            </router-link> 
        </div>
    </div>
    <div v-else>
        <h1>Loading ... </h1>
    </div>

</template>

<script>
export default {
    data() {
        return {
            events: []
        }
    },
    mounted() {
        fetch('http://localhost:3000/v1/event')
        .then(res => res.json())
        .then(data => this.events = data.events)
        .catch(err => consol.log(err.message))
    }
}
</script>

<style>
    .event{
        background: #f4f4f4;
        padding: 20px;
        border-radius: 3px;
        margin: 10px auto;
        max-width: 500px;
        cursor: pointer;
    }
    .event h2,p{
        color: #444;
    }
    .event:hover{
        background: #ddd;
    }
    .event a{
        text-decoration: none;
    }
</style>