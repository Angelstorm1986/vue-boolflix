<template>
    <section>
        <h2>{{title}}</h2>
        <ul>
            <li v-for="(item) in items" :key="item.id">
            id: {{item.id}}
            titolo originale: {{item.original_title ? item.original_title : item.original_name}}
            titolo: {{item.title ? item.title : item.name}}
            lingua: {{item.original_language}}
            <img v-if="item.original_language === 'en' || item.original_language === 'it'" :src="require('../assets/images/' + item.original_language + '.jpg')" :alt="'Bandiera' + item.original_language">
            <img v-else :src="require('../assets/images/' + flag + '.jpg')" :alt="'Bandiera' + flag">
            voto: {{item.vote_average}}
            </li>
        </ul>
    </section>
</template>

<script>
export default {
    name: 'AppGrid',
    props:{
        items: Array,
        loader: Boolean,
        title: String
    },
    data(){
        return {
            flag: 'generica'
        }
    }
}
</script>

<style lang="scss">
img{
    max-width: 100px;
}
</style>