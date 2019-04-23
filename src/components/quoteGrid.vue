<template>
    <div>
        <div v-for="(quotee,index) in quotes" :key="index" :qts="quotes" @click="dele(index)">
            <app-quote>
                {{ quotee }} 
            </app-quote>
        </div>
    </div>
</template>

<script>
import quote from './quote.vue';
import { eventBus } from '../main.js'

export default {
    props : ['quotes','number'],
    components : {
        appQuote : quote
    },
    data(){
        return {myN : this.number}
    },
     watch: {
        number : function(){
            this.myN = this.number
        }
    }, 
    methods : {
        dele(val){
            this.quotes.splice(val,1);
            this.myN--;
            eventBus.$emit('numberChanged',this.myN);
            
        }
    }
}
</script>

<style>

</style>
