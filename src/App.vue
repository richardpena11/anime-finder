<template>
  <div id="app">

    <section class="searchBox">
      <form>
        <input 
            type="text" 
            class="input_name"
            placeholder="Search..."
            v-model="query">

        <select 
          name="type"
          class="select_type"
          v-model="type">
          <option 
            v-for="(type, index) in optionsType" 
            :key="index"
            >{{type}}
          </option>
        </select>

        <button 
          @click.prevent="fetchSearch"
          class="btn_search"
        >Submit</button>
      </form>
    </section>

    <compResults
      v-if="data"
      :data="data.results"
      :type="type"
    />

    <compError
      v-if="error"
      :error="error"
    />

  </div>
</template>

<script>
  import compResults from './components/Results.vue'
  import compError from './components/Error.vue'

  export default {
    name: 'App',

    components: {
      compResults,
      compError
    },

    data() {
      return {
        query: '',
        type: 'anime',
        optionsType: [
          'anime',
          'manga',
          'character'
        ],
        baseURL: 'https://api.jikan.moe/v3/',
        data: null,
        error: null
      }
    },

    methods: {

      fetchSearch(){

        this.data = null
        this.error = null
        this.query = this.query.split(" ")
        this.query = this.query.join("%20")

        console.log(`${this.baseURL}search/${this.type}?q=${this.query}`)
        
        fetch(`${this.baseURL}search/${this.type}?q=${this.query}`)
        .then( response => response.json())
        .then( data => {
            if (data.results){
              this.data = data
            } else if(data.error){
              this.error = data
            }
            console.log(this.data)
        })

        this.query = ""
      }
    },
  }

</script>

<style>

  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Roboto', sans-serif;
  }

  body{
    background: url('./assets/bg.jpg');
    background-attachment: fixed;
    background-size: cover !important;
    color: #fff;
  }

  #app{
    width: 95%;
    max-width: 1300px;
    min-height: 100vh;
    padding: 20px 0px;
    margin: 0 auto;
  }

  .searchBox{
    width: 100%;
  }

  .searchBox form{
    width: 100%;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }

  .searchBox form .input_name{
    width: calc(100% - 300px);
    height: 60px;
    padding: 10px;
    border-radius: 6px;
    outline: none;
    border: 2px solid #000;
    font-size: 20px;
  }

  .searchBox form .select_type{
    width: 150px;
    height: 60px;
    padding: 10px;
    font-size: 20px;
    border-radius: 6px;
    text-transform: capitalize;
    outline: none;
    border: 2px solid #000;
  }

  .searchBox form .btn_search{
    width: 120px;
    height: 60px;
    padding: 10px;
    font-size: 20px;
    border-radius: 6px;
    color: #fff;
    background: #4f6d44;
    outline: none;
    border: none;
  }

  @media screen and (max-width: 525px){

    .searchBox form .input_name{
      width: calc(100% - 220px);
    }

    .searchBox form .select_type{
      width: 120px;
    }

    .searchBox form .btn_search{
      width: 90px;
      height: 60px;
      padding: 10px;
      font-size: 20px;
      border-radius: 6px;
      color: #fff;
      background: #4f6d44;
      outline: none;
      border: none;
    }
  }

  @media screen and (max-width: 360px){

    .searchBox form .input_name{
      width: 100%;
      margin-bottom: 5px;
    }

    .searchBox form .select_type{
      width: calc(100% - 125px);
    }

    .searchBox form .btn_search{
      width: 120px;
    }
  }

</style>