<template>
    <div>
        <h1> {{ num }}  {{ upper }} </h1>
        <small>{{ url }}</small>
    </div>
</template>

<script>
  import axios from 'axios';
    export default {
        props: {
            num: Number,
            name: String,
            url: String
        },
        computed: {
            upper: function(){
                var newName = this.name[0].toUpperCase() + this.name.slice(1);
             return newName;
        },
}}
</script>

<style>

</style>