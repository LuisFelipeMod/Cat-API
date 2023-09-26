<script setup>
import { onMounted, reactive, ref } from 'vue'

let cats = reactive(ref());

onMounted(() =>{
  fetch("https://api.thecatapi.com/v1/breeds")
  .then(response => response.json())
  .then(response => {
    cats.value = response
    console.log(cats.value)
  });

})

</script>

<template>
  <div>
    <ul>
      <li v-for="breed in cats" :key="breed">
        <img :src="'https://cdn2.thecatapi.com/images/'+breed.reference_image_id+'.jpg'"> <br/>
        <span :href="breed.wikipedia_url">
            <strong>Breed:</strong>
            {{ breed.name }}<br>
            <strong>Temperament:</strong>
            {{ breed.temperament }} <br>
            <strong>About the breed:</strong>
            {{ breed.description }} <br>
            <strong>See More In Wikipedia:
              <a :href="breed.wikipedia_url">
                {{ breed.wikipedia_url }}
              </a>
            </strong>
        </span>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  ul{
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
  }
  li{
    width: 45%;
    margin-bottom: 2rem;
    list-style-type: none;
  }
  img{
    margin-top: 1rem;
    max-width: 100%;
    height: 372px;
    object-fit: contain;
  }
  span{
    display: flex;
    flex-direction: column;
  }
  strong{
    margin-top: 0.5rem;
  }
</style>
