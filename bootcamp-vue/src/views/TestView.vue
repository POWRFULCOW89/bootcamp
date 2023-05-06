<template>
    <div>
        <h1>Variable: {{ counter }}</h1>
        <button @click="increment">Aumentar</button>

        <ul>
            <li v-for="n in array">{{ n }}</li>
        </ul>

        <h3>{{ fullName }}</h3>
    </div>
</template>

<script>
export default {
    name: "TestView",
    data() {
        return {
            counter: 1,
            array: Array(5).fill(0).map(Math.random),
            firstName: "Diego",
            lastName: "Melo"
        }
    },
    methods: {
        increment() {
            this.counter++;
        }
    },
    computed: {
        fullName(){
            return `${this.firstName} ${this.lastName}` 
        }
    }
}
</script>

<style scoped>
div {
    border: 1px solid white;
    border-radius: 100px;
    padding: 2.5em
}

button {
    padding: .75em;
    font-size: 1rem;
    margin: 0 auto;
    display: block;
}

ul {
    margin: 2em 1em;
}
</style>