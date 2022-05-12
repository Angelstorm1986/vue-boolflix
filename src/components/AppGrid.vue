<template>
    <section>
        <h2>{{title}}</h2>
        <ul class="row">
            <li class="col-sm-6 col-md-3 col-lg-2" v-for="(item) in items" :key="item.id">
            id: {{item.id}}<br>
            titolo originale: {{item.original_title ? item.original_title : item.original_name}}<br>
            titolo: {{item.title ? item.title : item.name}}<br>
            lingua: <img v-if="item.original_language === 'en' || item.original_language === 'it'" :src="require('../assets/images/' + item.original_language + '.jpg')" :alt="'Bandiera' + item.original_language">
            <img v-else :src="require('../assets/images/' + flag + '.jpg')" :alt="'Bandiera' + flag"><br>
            voto: {{item.vote_average}}<br>
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
    max-width: 20px;
}
</style>