<template>
    <div >
        <input type="text" v-model="search"
               @input="update" class="form-control border "  placeholder="Search stories by title, url or author" >


    </div>
</template>

<script>

    import {EventBus} from "../../main";

    export default {
    data: ()=>{
    return {
        search: '',
        List: []
    }
    },
    methods: {
        update: function(){
            EventBus.$emit('search', this.search)
        }

    },


    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped >
    body {

    }
    #tc {
        color: grey;
    }

</style>
