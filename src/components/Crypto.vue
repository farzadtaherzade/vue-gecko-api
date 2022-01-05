<template>
  <div class="crypto">
    <form>
      <h1>Search a currency</h1>
      <input type="search" placeholder="Search" class="search" v-model="input" @keyup="filterCurrency">
    </form>

    <div class="coin-container">
      <div class="coin-row" v-for="coin in coins" :key="coin.id">
        <div class="coin">

          <img :src="coin.image" :alt="coin.id" class="coin-img">
          <h4 class="coin-name">{{coin.name}}</h4>
          <small class="coin-symbol">{{coin.symbol.toUpperCase()}}</small>

        </div>
        
        <div class="coin-info">

          <p class="coin-current_price color">${{coin.current_price.toLocaleString()}}</p>
          <p class="coin-total_volume color">${{coin.total_volume.toLocaleString()}}</p>
          <p class="coin-price_change_percentage_24h" :class="{ 'red' :coin.price_change_percentage_24h, 'green':coin.price_change_percentage_24h > 0 }">{{coin.price_change_percentage_24h.toFixed(1)}}%</p>
          <p class="coin-market_cap color">{{coin.market_cap.toLocaleString()}}</p>

        </div>
      </div>
    </div>


  </div>
</template>

<script>
import axios from 'axios'
import {ref} from 'vue'
export default {
  setup() {
      
      const coins = ref([])
      const input = ref('')

      axios
        .get("https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false")
        .then(function (response) {
            coins.value = response.data
        })
        .catch(function (error) {
          alert(error)
        })
      
      
      function filterCurrency() {
      //
        if (input.value === "") {
            axios
          .get("https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false")
          .then(function (response) {
              coins.value = response.data
          })
          .catch(function (error) {
            alert(error)
        })
        }else{
          axios
        .get("https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false")
        .then(function (response) {
          coins.value = (response.data.filter((coin) => coin.name.toLowerCase().includes(input.value.toLowerCase())))
        })
        .catch(function (error) {
          alert(error)
        })
        }
      }

      return { coins , input , filterCurrency}
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>  


  .crypto{
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top:2rem ;
  }

  .coin-container{
    display: flex;
    flex-direction: column;
    /* margin: 12px 20rem 10px 20rem ; */
  }

  .coin-row{
    display: flex;
    flex-direction: row;
    justify-content: start;
    align-items: center;
    border-bottom: 1px solid rgb(125, 73, 221);
    width: 900px;
    height: 80px;
    margin-bottom: 20px;
  }

  .coin-info{
    display: flex;
    flex-direction: row;
    text-align: center;
    justify-content: space-between;
    width: 100%;
  }

  .coin-info > p{
    margin-right: 2rem ;
    font-size:0.9rem ;
  }

  .color{
    color: #989898;
  }

  .coin{
    display: flex;
    align-items: center;
    min-width: 300px;
    padding-right: 24px;
  }

  .coin > small{
    color: #989898;
  }

  .coin > h4{
    width: 150px;
    margin-right: 20px;
  }

  .coin-img{
    width: 18px;
    height: 18px;
    margin-right: 10px;
  }

  .search{
    width: 100%;
    padding: 10px;
    line-height: 1.5;
    border: 1px solid #636363;
    background-color: #111!important;
    color: #989898;
    background-color: #6441a5 ;
    transition: 0.3s;
    outline: none;
    margin-top: 15px;
    margin-bottom: 15px;
  }

  .search[type=search]::placeholder{
    color: #989898;
  }
  .search[type=search]:focus{
    border: 2px solid #8dc647!important;
    box-shadow: none!important;;
    color: #989898;
  }

  .red{
    color: red;
  }.green{
    color: green;
  }
</style>
