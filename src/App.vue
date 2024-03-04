<template>
<!--Navbar-->
  <Navbar/>

  <Event :text="text" />
  <Searchbar
      :data="data_temp"
      @searchMovie="searchMovie($event)"
  />
<!--body contents-->
  <Movies
    :data="data_temp"
    @openModal="isModal=true; selectedMovie=$event"
    @increaseLike="increaseLike($event)"
  />

<!--Modal 컴포넌트-->
  <Modal
      :data="data"
      :isModal="isModal"
      :selectedMovie="selectedMovie"
      @closeModal="isModal=false"/>

</template>

<script>
import {data} from '../public/assets/movies.js';
import Navbar from './components/Navbar.vue';
import Searchbar from './components/Searchbar.vue';
import Event from './components/Event.vue';
import Movies from './components/Movies.vue';
import Modal from './components/Modal.vue';
console.log(data)

  export default {
    name: 'App',
    data(){
      return {
        isModal: false,
        foods: ['김밥', '순대', '만두'],
        selectedMovie: 0,
        data: data,
        data_temp: [...data],
        text: "NEPLIX 강렬한 운명의 드라마, 경기크리처"
      }
    },
    methods:{
      increaseLike(i){
        this.data[i].like += 1;
      },
      searchMovie(title){
        this.data_temp = this.data.filter(movie =>{
          return movie.title.includes(title);
        })
      }
    },
    components:{
      Navbar: Navbar,
      Searchbar: Searchbar,
      Event: Event,
      Movies: Movies,
      Modal: Modal,
    }
  }
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}

body {
  max-width: 768px;
  margin: 0 auto;
}

h1,
h2,
h3 {
  margin-bottom: 1rem;
}

p {
  margin-bottom: 0.5rem;
}

button {
  margin-right: 10px;
  margin-top: 1rem;
}

.item {
  width: 100%;
  border: 1px solid #ccc;
  display: flex;
  margin-bottom: 20px;
  padding: 1rem;
}

.item figure {
  width: 30%;
  margin-right: 1rem;
}

.item img {
  width: 100%;
}

.item .info {
  width: 100%;
}

.modal {
  background: rgba(0, 0, 0, 0.7);
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal .inner {
  background: #fff;
  width: 80%;
  padding: 20px;
  border-radius: 10px;
}

  .bg-yellow{
    background-color: yellow;
  }
</style>
