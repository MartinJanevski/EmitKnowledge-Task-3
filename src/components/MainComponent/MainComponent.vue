<template>
    <div>
    <div v-for="item of filteredPosts" v-bind:key="item.id" id="App" >

        <div class="card">
            <div class="card-body">
                <div v-if="item.type=='story'">
                    <h6 class="text-left">{{item.title}}</h6>


                    <span class="small">Likes: {{item.score}} </span>
                    <span class="small" >  Author: {{item.by}} </span>
                    <span class="small">Time : {{TimeConverter(item.time)}}</span>
                    <span class="small"> <a v-bind:href="item.url">{{item.url}}  </a> </span>
                    <span class="text-right">Comments: {{item.descendants}}</span>
                    <span class="small">               Type: {{item.type}}    </span>
                </div>
            </div>
        </div>

    </div>
    </div>
</template>
<style>


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
        }

    }

</script>


<style >

</style>
