<template>
    <div class="d-flex justify-content-end align-items-center">
      <input class="search" type="text" placeholder="Cerca Film e Serie TV..." v-model="search" @input="cerca">
      <i @click="cerca" class="fa-solid fa-magnifying-glass"></i>
      <i @click="reset" class="fa-solid fa-arrow-rotate-left"></i>
    </div>
</template>

<script>
export default {
    name: 'AppSearch',
    data(){
        return {
           search: ''
        }
    },
    methods:{
        cerca(){
            this.$emit('performSearch',this.search);
        },
        reset(){
            this.search = '';
        }
    }
}
</script>

<style lang="scss">
@import '../styles/vars.scss';
div{
    margin-right: 20px;
    .search{
        border: none;
        background-color: $bg-color;
        outline: none;
        color: $base-color;
    }
    ::placeholder {
        opacity: 0.5;
        color: $base-color;
    }
    .fa-magnifying-glass,
    .fa-arrow-rotate-left{
        color: $base-color;
        margin-left: 10px;
        cursor: pointer;
    }
}

</style>