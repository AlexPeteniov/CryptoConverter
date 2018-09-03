<template>
  <div id="app">
    <h1>{{ msg }}</h1>

    <img src="./assets/anonymous.gif">
    <div id = "databinding" style = "">
      <h1>Currency Converter</h1>
      <span>Enter Amount:</span><input type = "number" v-model.number = "amount" placeholder = "Enter Amount" /><br/><br/>
      <span>Convert From:</span>
      <select v-model = "convertfrom" style = "width:100px;font-size:25px;">
        <option v-for = "(result, index) in results"
                v-bind:value = "result"
        >{{result.name}}</option>
      </select>
      <span>Convert To:</span>
      <select v-model = "convertto" style = "width:100px;font-size:25px;">
        <option v-for = "currency in currencys" v-bind:value = "currency.desc">
          {{currency.name}}</option>
      </select><br/><br/>
        <span  v-if ="convertto=='US Dollar'">
        {{amount}} {{convertfrom.name}} equals {{amount*convertfrom.quotes.USD.price|currencydecimal}} {{convertto}}</span>
        <span  v-else-if ="convertto=='Euro'">
        {{amount}} {{convertfrom.name}} equals {{amount*convertfrom.quotes.EUR.price|currencydecimal}} {{convertto}}</span>



    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to CryptoCurrency Converter',
      currencys: [
        {name : "USD", desc:"US Dollar"},
        {name:"EUR", desc:"Euro"},

      ],
      convertfrom:'BIT',
      convertto:'',
      amount :'',
      info:'',
      results:''
    }

  },
  filters: {
    currencydecimal (value) {
      return value.toFixed(2)
    }
  },
  mounted() {

    axios
      .get('https://api.coinmarketcap.com/v2/ticker/?convert=EUR&limit=10')
      .then(response => (this.results = response.data.data));
  /*  axios
      .get('https://api.coinmarketcap.com/v2/ticker/?convert=EUR&limit=10')
      .then(response => (this.USDs = response.data.data.quotes.USD.price));
    axios
      .get('https://api.coinmarketcap.com/v2/ticker/?convert=EUR&limit=10')
      .then(response => (this.EUR = response.data.data.quotes.))*/

  }
}
</script>

<style lang="scss">
  body {
    width:100%;
    height:100%;
    background-image: url('https://media.giphy.com/media/vc2H0gN8Kl2Lu/giphy.gif');
    background-size: cover;
    margin:0}


#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #FE880C;

}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 15px;
  margin: 0px;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
