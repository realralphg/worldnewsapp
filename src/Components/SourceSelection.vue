<template>
    <div class="container">                
            <img src="../assets/ralphpaw.png">
            <h3>World News App</h3>            

        <select class="form-control select-bar" @change="sourceChanged">
            <option v-for="source in sources" :key="source.id" :value="source.id">{{source.name}}</option>
        </select>

        <div v-if="!source">
            <span>Select your preferred News Channel from the options</span>
        </div>
     
        <div v-if="source">
            <h6>{{source.description}}</h6>
            <a :href="source.url" target="blank"> Go to {{source.name}}</a>
        </div>
        
        <!-- Add Corona Cases -->
        
        <!-- <div class="corona">
            {{corona}}
        </div> -->
    </div>
</template>

<script>
name: 'sourceSelection'

    export default {
        data(){
            return{
                sources: [],
                source: '',
                corona: []
            }
        },

        methods:{
            sourceChanged(e){                                            
                this.sources.map(record =>{
                    if (record.id == e.target.value) {
                        this.source = record
                    }                    
                })
                this.$emit('sourceChanged', e.target.value)
            }
        },

        created() {
            this.$http.get('https://newsapi.org/v1/sources?language=en')                    
                .then(response => {                    
                    this.sources = response.data.sources
                })
            
            // this.$http.get('https://api.covid19api.com/dayone/country/nigeria/status/confirmed')
            //     .then(response =>{
            //         this.corona = response.data
            //         console.log(this.corona)
            //     }) 
        }
    }
</script>

<style scoped>
    body{
        color: white
    }
    .container{
        background-color: rgb(43, 1, 1);
        padding: 10px;
    }
    .select-bar{
        top: 30px;
        right: 0;
        left: 0;
        width: 100%;        
        font-size: 1.2rem;
        background-color: teal;
        color: white;
    }

    a {
        text-decoration: none;
        color: white;
        border-radius: 10px; 
        background: teal;
        padding: 5px;
    }

    span{
        color: white;
        padding-top: 20px;
        font-size:0.8rem;
    }

    h3{
        color: white;
        
    }

    h6{
        color: white;
    }
    img{
        float: right;
        padding: 0px;
    }
    .corona{
        color: white;
    }
</style>