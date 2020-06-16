<template>
    <div>
    <div v-for="item of filteredPosts" v-bind:key="item.id" id="App" >
        <div >

            <div class="card ">
                <div class="card-body">
                    <div v-if="item.type=='story'" >
                    <blockquote class="blockquote ">

                        <a class="text-black-50" :href="item.url">
                               <div class="text-left">{{item.title}}</div>
                             </a>


                        <footer class="blockquote-footer text-left ">
                                <div class="text-right">
                                    <span class="text-right "> <a href="#" class="badge badge-dark align-top   ">{{item.descendants}}</a> </span>
                                    <span class="small lnr lnr-location m-4">   </span>
                                    <span class="lnr lnr-star"></span>
                                </div>
                            <cite title="Source Title" class="text-left">
                                <span class=" lnr lnr-heart"> {{item.score}}   </span>
                                <span class=" lnr lnr-user" >  {{item.by}}   </span>
                                <span class="lnr lnr-clock">  {{TimeConverter(item.time)}}     </span>
                                <span class=""> <a v-bind:href="item.url">{{item.url}}    </a> </span></cite>
                        </footer>
                    </blockquote>
                    </div>
                </div>
            </div>

        </div>
    </div>
    </div>
</template>
<style scoped>




</style>
<script>

    import {EventBus} from'../../main.js'
    export default {
        props:{


        },
        data: () =>{
            return {
             List: [],
             search: ''
            }
        },
        created () {
            EventBus.$on('search',(value)=>{
                this.search=value;
            })

            EventBus.$on('ListItems',(value)=>{
                this.List=value;
            })

        },
        methods: {
            TimeConverter: function (unix_timestamp) {
                {
                    var date = new Date(unix_timestamp * 1000);
                    var hours = date.getHours();
                    var minutes = "0" + date.getMinutes();
                    var seconds = "0" + date.getSeconds();
                    var formattedTime = hours + ':' + minutes.substr(-2) + ':' + seconds.substr(-2);
                    return (formattedTime);            }
            },
            clearList(){
                return (this.List=[],
                 this.search='')
            }


        },
        computed:{
            filteredPosts: function(){
                var filteredList=this.List.filter((item)=>{
                    return ( (item.title.toLowerCase().match(this.search.toLowerCase()))||
                        (item.by.toLowerCase().match(this.search.toLowerCase()))
                    );
                })
                return filteredList;

            }
        },
        mounted(){
            this.clearList();

        }

    }

</script>


<style >

</style>
