<template>
    <section class="container">
        <div class="row gy-3">
            <div class="card-cicle col-sm-6 col-md-4 col-lg-3 col-xl-2 mx-0" v-for="(item) in items" :key="item.id">
                <img class="image-film" :src="imagePath + item.poster_path" alt="">
                <div class="overlay">
                    <span>{{ item.id }}</span>
                    <h4>{{ item.title ? item.title : item.name }}</h4>
                    <p>{{ item.release_date }}</p>
                    <p>{{ item.overview }}</p>
                    <img class="image-flag" v-if="item.original_language === 'en' || item.original_language === 'it'" :src="require('../assets/images/' + item.original_language + '.jpg')" :alt="'Bandiera' + item.original_language">
                    <img class="image-flag" v-else :src="require('../assets/images/' + flag + '.jpg')" :alt="'Bandiera' + flag">
                    <div>
                        <span v-for="numero in 5" :key="numero">
                            <i :class="numero <= (Math.ceil(item.vote_average / 2)) ? 'fa-solid fa-star voted' : 'fa-regular fa-star'"></i>
                        </span>
                    </div>
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
    div{
        .card-cicle{
            color: $base-color;
            position: relative;
            max-height: 350px;
            .image-film{
                max-height: 400px;
                height: 100%;
                width: 100%;
            }
            .overlay{
                width: 100%;
                background-color: rgba(0,0,0);
                top: 0;
                left: 0;
                right: 0;
                bottom: 0;
                position: absolute;
                display: none;
                padding: 20px;
                overflow-y: auto;
                .image-flag{
                    max-width: 20px;
                }
            }
        }
    }
}
.card-cicle:hover .overlay{
    display: block;
}
</style>