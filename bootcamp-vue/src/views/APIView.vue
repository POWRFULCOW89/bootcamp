<template>
    <div>
        <h1>Rick and Morty API</h1>

        <form @submit.prevent="">
            <label for="name">Nombre</label>
            <input @input="debounceSubmit" autocomplete="off" id="name" v-model="name" />
            <!-- <button type="submit">Enviar</button> -->
        </form>

        <div id="error" v-if="error">
            <p>No se pudo encontrar el personaje</p>
        </div>

        <div id="character" v-else-if="character">
            <div v-if="characters.length > 1" id="pagination">
                <button @click="first">&larrb;</button>
                <button @click="prev" :disabled="!character.id">&leftarrow;</button>
                <div id="pagination-numbers">
                    <button @click="setCharacter(index)" v-for="(character, index) of characters">
                        {{ index + 1 }}
                    </button>
                </div>
                <button @click="next">&rightarrow;</button>
                <button @click="last">&rarrb;</button>
            </div>

            <h2>{{ character.name }} - #{{ character.id }}</h2>
            <img :src="character.image" />
            <table>
                <tr v-for="field in fields">
                    <th>
                        {{ capitalize(field) }}
                    </th>
                    <td>
                        {{ character[field] }}
                    </td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    name: "APIView",
    data() {
        return {
            characters: null,
            error: null,
            name: "",
            characterIndex: 0,
            fields: [
                "status", "species", "gender"
            ],
            timeout: null
        }
    },
    computed: {
        character() {
            if (this.characters) return this.characters[this.characterIndex];
        }
    },
    methods: {
        async submit() {
            try {
                this.error = null;
                let res = await fetch(`https://rickandmortyapi.com/api/character/?name=${this.name}`)
                let data = await res.json();
                console.log(data)
                if (data.error) throw new Error(data.error);
                this.characters = data.results
                this.characterIndex = 0
            } catch (error) {
                this.error = error
            }
        },
        capitalize(string) {
            return string[0].toUpperCase() + string.slice(1)
        },
        debounceSubmit() {
            clearTimeout(this.timeout)
            this.timeout = setTimeout(this.submit, 1000)
        },
        setCharacter(index) {
            this.characterIndex = index;
        },
        first() {
            this.characterIndex = 0
        },
        prev() {
            if (this.characterIndex > 0) this.characterIndex--;
        },
        next() {
            if (this.characterIndex < this.characters.length - 1) this.characterIndex++
        },
        last() {
            this.characterIndex = this.characters.length - 1;
        }

    },
}
</script>

<style scoped>
#pagination,
#pagination-numbers {
    display: flex;
    gap: 0.25em;
    /* padding: .25em; */
    font-size: 18px;

}

#pagination button {

    background-color: transparent;
    color: white;

    border: 1px solid white;
}

#character {
    padding: 2em 0;
    border-radius: 16px;
    border: 1px solid white;
    box-shadow: 5px 5px 5px rgba(255, 255, 255, .5);
}

#error {
    font-size: 28px;
    display: block;
    margin: 0 auto;
    text-align: center;
}

h1 {
    text-align: center;
    margin: 1.5em;
}

form {
    display: flex;
    margin: 2em;
}

form label {
    flex: 1;
    text-align: right;
}

form input {
    flex: 2
}

form button {
    flex: .5
}

form>* {
    padding: .5em;
    font-size: 16px;
}

h3 {
    text-align: center;
    text-decoration: underline;
}

img {
    border-radius: 100%;
    width: 40%;
    margin: 2em;
}

#character {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1em;
}

table {
    text-align: left;
}

table,
table td,
table th {
    border: 1px solid #eee;
    /* padding: .25em; */
}

table td,
table th {
    padding: .4em .8em;
    font-size: 22px;
}

table th {
    font-weight: 700;
}
</style>