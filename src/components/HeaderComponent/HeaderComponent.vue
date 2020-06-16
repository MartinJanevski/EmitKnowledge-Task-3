<template>
    <div>

        <nav class=" sb-topnav navbar navbar-expand-md navbar-light bg-white">
            <div class="d-flex flex-grow-1">
                <a class="navbar-brand" href="index.html"> <img class="logo" src="./logo.png"><span id="banertext" >Search Hacker News</span ></a>
                <form class="mr-2 my-auto w-100 d-inline-block order-1">
                        <div class="form-control border-0 border-right-0">
                            <SearchComponent></SearchComponent>
                        </div>


                </form>
            </div>

        </nav>




    </div>
</template>

<script>
    import SearchComponent from "./SearchComponent";
    export default {
    components: {
        SearchComponent
    }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .logo {
        width: 50px;
    }
    .navbar{padding-bottom: 0px;}
    span {
        height: 20px;
    }
    #banertext {
        font-size: 15px;
        color: grey;
    }

</style>
