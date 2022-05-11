<template>
    <div>
      <input type="text" placeholder="Cerca film e serie TV" v-model="search" @keyup.enter="cerca">
      <button @click="cerca">Cerca</button>
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
            this.search = '';
        }
    }
}
</script>

<style lang="scss">

</style>