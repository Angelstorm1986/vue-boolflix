<template>
    <section class="container">
        <h2>{{title}}</h2>
        <div class="row gy-3">
            <div class="card col-sm-6 col-md-3 col-lg-2" v-for="(item) in items" :key="item.id">
                <img class="image-film" :src="imagePath + item.poster_path" alt="">
                <span>{{item.id}}</span>
                <h4>{{item.title ? item.title : item.name}}</h4>
                <span><img class="image-flag" v-if="item.original_language === 'en' || item.original_language === 'it'" :src="require('../assets/images/' + item.original_language + '.jpg')" :alt="'Bandiera' + item.original_language">
                <img class="image-flag" v-else :src="require('../assets/images/' + flag + '.jpg')" :alt="'Bandiera' + flag"></span>
                <div>
                    <span v-for="numero in 5" :key="numero">
                        <i :class="numero <= (item.vote_average / 2) ? 'fa-solid fa-star voted' : 'fa-regular fa-star'"></i>
                    </span>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    name: 'AppGrid',
    props:{
        items: Array,
        loader: Boolean,
        title: String,
    },
    data(){
        return {
            imagePath: 'https://image.tmdb.org/t/p/w342',
            flag: 'generica'
        }
    },
}
</script>

<style lang="scss">
@import '../styles/vars.scss';
section{
    margin-top: 30px;
    h2{
        color: $base-color; 
    }
    div{
        .card{
            padding: 20px;
            background-color: $bg-card;
            color: $base-color;
            .image-film{
                max-height: 400px;
            }
            .image-flag{
                max-width: 20px;
            }
        }
    }
}
</style>