<template>
    <h1>{{ formName }}</h1>
    <form @submit.prevent="submit">
        <label for="name">Nombre</label>
        <input id="name" v-model="name" />

        <label for="email">Email</label>
        <input id="email" v-model="email" />

        <div v-if="showAge">

            <label for="age">Edad</label>
            <input id="age" v-model="age" />

        </div>

        <p v-else>Sin edad</p>

        <button type="submit">Enviar</button>
    </form>
</template>

<script>
export default {
    setup() {

        console.log("setup")
        return {}
    },
    props: {
        formName: {
            type: String,
            required: true
        },
        showAge: {
            type: Boolean,
            default: true
        }
    },
    data() {
        return {
            name: "",
            email: "",
            age: ""
        }
    },
    methods: {
        submit() {
            console.log(`${this.name} | ${this.email}`);
        }
    }
}
</script>

<style lang="scss" scoped></style>