<template>
    <div>
        Nuevo componente
        <p>{{$data }}</p>

        <p :class="{hide: bool}">Título</p>
    </div>
</template>

<script>
// import { mapStores } from 'pinia';
// import useCounterStore from "../stores/counter";

//     export default {
//         name: "Component",
//         data(){
//             return {
//                 bool: true
//             }
//         },
//         computed: {
//             ...mapStores(useCounterStore)
//         },
//         methods: {
//             action(){
//                 // this.counterStore.
//             }
//         }
//     }
</script>

<style scoped>
.hide {
    display: none;
}
</style>