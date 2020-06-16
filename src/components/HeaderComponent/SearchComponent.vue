<template>
    <div >

            <input type="text" id="tc"
                   v-model="search"
                   @input="update"
                   class="form-control navbar-text mx-md-4"
                   placeholder="Search stories by title, url or author" style="width:200px">
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
