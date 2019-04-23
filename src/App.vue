<template>
  <div id="app">
    <div class="cont">
      <h2>Progress - Number of Quotes</h2>  
    <div id="big">
      <div id="small"  :style="{width:currentNumberOfQuotes * 10 +'%'}" :class="[ isZero ? 'ree' :'gree' ]">
        {{currentNumberOfQuotes}} / 10
      </div>
    </div>
    </div>
    <div class="section">
      <div> <textarea v-model="content" cols="50" rows="10"></textarea></div>
      <div> <button class="btnAdd" @click="addQuote">Add Quote</button></div>
    </div>
    <div>
    <app-quote-grid style="display : block;" :quotes="quotes" :number="currentNumberOfQuotes"></app-quote-grid>
    </div>
    
    <footer class="footer">
      You can Click on Any Quote to delete it (if You access the maximun number of Quotes)
    </footer>
  </div>


</template>

<script>
import quoteGrid from './components/quoteGrid.vue';
import { eventBus } from './main.js'
  export default {
    components :{
      appQuoteGrid : quoteGrid
    },
    data(){
      return {
        maxQ : 10,
        quotes : [],
        currentNumberOfQuotes : 0,
        content : '',
        isZero : true
      }
    },
    methods:{
      addQuote(){
        if(this.currentNumberOfQuotes < this.maxQ)
        {
          this.quotes.push(this.content);
          this.currentNumberOfQuotes++;
          this.content = '';
          this.isZero = false;
       
        } else {
          alert('You reached to the maximum number of Quotes .. You should delete quotes to be able to add Quotes!!')
        }
      }
    },
    created(){
      eventBus.$on('numberChanged', (number) => {
        this.currentNumberOfQuotes = number;
        console.log(this.currentNumberOfQuotes)
        if(this.currentNumberOfQuotes === 0)
        {
          this.isZero = true;
        } 
        
      });
    }

    
  }
</script>

<style scoped>
  #big {
    width: 1100px;
    height: 20px;
    background-color: #3393df;
    border-radius: 7px;
  }

  #small {
    height: 20px;
    text-align: center;
    min-width: 40px;
    border-radius: 7px;
    color: white;
  }

  .cont{
    margin: 10px;
  }
  .section{
    display: inline-flex;
    margin-bottom: 40px;
  }
  .btnAdd{
    margin: 116px 0px 0px 27px;
    background-color: #3393df;
    -moz-border-radius: 28px;
    -webkit-border-radius: 28px;
    border-radius: 11px;
    border: 1.2px solid #010101;
    display: inline-block;
    cursor: pointer;
    color: #ffffff;
    font-family: Arial;
    font-size: 17px;
    padding: 10px 31px;
    text-decoration: none;
    text-shadow: 0px 1px 0px #2f6627
   }
   
  .gree {
    background-color: #be3b13;
  }
  .ree {
    background-color: #3393df;
  }

  h2{
    margin-bottom: 7px;
  }
  .footer{
    margin: 80px 0 0px 440px;
    padding: 20px;
    background-color: #3393df;
    border-radius: 9px;
    text-align: center;
    display: inline-block;
  }

</style>
