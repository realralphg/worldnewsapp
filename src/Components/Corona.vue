<template>
    <div>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                corona: []
            }
        },

        created(){            
            this.$http.get('https://api.covid19api.com/summary')
                .then(response =>{
                    this.corona = response
                    console.log(corona)
                })  
        }
    }
</script>

<style lang="scss" scoped>

</style>