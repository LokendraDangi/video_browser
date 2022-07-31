<template>
    <div>
          <input @input="onInput" />
          <!-- <input v-on:input="onInput" /> -->

    </div>
</template>

<script>
    export default {
        name: 'SearchBar',
        methods: {
            onInput: function(event){
                this.$emit('termChange', event.target.value);
                // console.log(event.target.value);
            }
        }
    };
</script>

<style scoped>
    input{
        width:75%;

    }
    div{
        text-align: center;
        margin:20px;
    }
</style>