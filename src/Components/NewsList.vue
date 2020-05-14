<template>
    <div class="container">
        <article v-for="(article, index) in articles" :key="index">            
            <header>
                <a :href="article.url" target="blank">
                    <img :src="article.urlToImage">
                </a>                 
            </header>
            <section>
                <h4><a :href="article.url" target="blank"> {{article.title}}</a></h4>
                <!-- <p> <small><i>By {{article.author}}</i> </small></p> -->
                <p>{{article.description}}</p>
            </section>                
        </article>
    </div>
</template>

<script>
    export default {
        props: ['source'],

        data() {
            return {
                articles: []
            }
        },

        methods:{
            //carries out updates of contents when called by watch
            updateSource: function(source){
                this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=c559acae585943ba9f5c803869100d55')
                    .then(response => {                    
                        this.articles = response.data.articles
                    })
            }
        },
        //watches out for any changes and calls updateSource function
        watch:{
            source: function(val){
                this.updateSource(val)
            }
        }
        
    }
</script>

<style scoped>
.container{
    padding-top: 10px;
    
}
article{
    display: grid;
    grid-template-columns: 100px auto;
    grid-template-rows: 100%;
    border-bottom: 1px solid lightslategray;
    overflow: hidden;
    cursor: pointer;
}
img{
    max-width: 100%;
    height: auto;
}
header{
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
}
section{
    margin: 0px;
    padding-left: 10px;
    height: auto;
    font-size: 0.8rem;
}
a {
    text-decoration: none;
    color: teal;
}
</style>