<template>
    <div>
        <br>
        <a class="nav-link" @click="ShowAll" v-bind:style="{cursor: selectedCursor}">
            <div class="sb-nav-link-icon">
                <i class="fas fa-chart-area"></i>
            </div>       All       </a>

        <a class="nav-link" @click="ShowHot" v-bind:style="{cursor: selectedCursor}">
            <div class="sb-nav-link-icon">
                <i class="fas fa-chart-area"></i>
            </div>       Hot       </a>

        <a class="nav-link" @click="ShowHN" v-bind:style="{cursor: selectedCursor}">
            <div class="sb-nav-link-icon">
                <i class="fas fa-chart-area"></i>
            </div>       ShowHN       </a>

        <a class="nav-link" @click="AskHN" v-bind:style="{cursor: selectedCursor}">
            <div class="sb-nav-link-icon">
                <i class="fas fa-chart-area"></i>
            </div>       AskHN       </a>

        <a class="nav-link" @click="AskHN" v-bind:style="{cursor: selectedCursor}">
            <div class="sb-nav-link-icon">
                <i class="fas fa-chart-area"></i>
            </div>       Polls       </a>

        <a class="nav-link" @click="AskHN" v-bind:style="{cursor: selectedCursor}">
            <div class="sb-nav-link-icon">
                <i class="fas fa-chart-area"></i>
                <hr>
            </div>       Jobs       </a>

        <a class="nav-link" @click="AskHN" v-bind:style="{cursor: selectedCursor}">
            <div class="sb-nav-link-icon">
                <i class="fas fa-chart-area"></i>
            </div>       Shipow       </a>

        <a class="nav-link" @click="AskHN" v-bind:style="{cursor: selectedCursor}">
            <div class="sb-nav-link-icon">
                <i class="fas fa-chart-area"></i>
            </div>       Stared       </a>









    </div>
</template>

<script>
    import {EventBus} from'../../main.js'
    import axios from "axios"
    export default {
        data() {
            return {
                List: [],
                idList: [],
                ShowHnList: [],
                selectedCursor: 'pointer'

            }
        },
        computed: {

        },
        methods:{
            ShowAll : function(){
                axios
                    .get('https://hacker-news.firebaseio.com/v0/newstories.json?print=pretty')
                    .then(response => {
                            this.idList = response.data;
                            for (let i = 0; i < 10; i++) {
                                let url = "https://hacker-news.firebaseio.com/v0/item/"
                                    + this.idList[i] + ".json";
                                axios.get(url).then(response => {
                                    this.List.push(response.data)
                                    EventBus.$emit('ListItems', this.List)



                                })

                            }
                        }
                    );
                this.List = []

            },
            ShowHot : function(){
                axios
                    .get('https://hacker-news.firebaseio.com/v0/beststories.json?print=pretty')
                    .then(response => {
                            this.idList = response.data;
                            for (let i = 0; i < 500; i++) {
                                let url = "https://hacker-news.firebaseio.com/v0/item/"
                                    + this.idList[i] + ".json";
                                axios.get(url).then(response => {
                                    this.List.push(response.data)
                                    EventBus.$emit('ListItems', this.List)
                                }); }
                        }
                    );
                this.List = []
            },
            ShowHN: function (){
                axios
                    .get('https://hacker-news.firebaseio.com/v0/beststories.json?print=pretty')
                    .then(response => {
                            this.idList = response.data;
                            for (let i = 0; i < 100; i++) {
                                let url = "https://hacker-news.firebaseio.com/v0/item/"
                                    + this.idList[i] + ".json";

                                axios.get(url).then(response => {
                                    if(response.data.title.startsWith('Show HN', 0))
                                    {this.List.push(response.data)}
                                    EventBus.$emit('ListItems', this.List)
                                });   }
                        }
                    );
                this.List = []
            },
            AskHN: function(){
                axios
                    .get('https://hacker-news.firebaseio.com/v0/beststories.json?print=pretty')
                    .then(response => {
                            this.idList = response.data;
                            for (let i = 0; i < 100; i++) {
                                let url = "https://hacker-news.firebaseio.com/v0/item/"
                                    + this.idList[i] + ".json";

                                axios.get(url).then(response => {
                                    if(response.data.title.startsWith('Ask HN', 0))
                                    {this.List.push(response.data)}
                                    EventBus.$emit('ListItems', this.List)
                                });   }
                        }
                    );
                this.List = []
            },


        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.nav-link{
    color: grey;
}


</style>
