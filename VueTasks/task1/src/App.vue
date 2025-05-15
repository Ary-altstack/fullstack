<script setup>
import { computed, ref } from "vue";
let searchTxt = ref(" ");
let title = "Welcome to Valtech Filtering app";
let ladyAvengers = ref([
  {
    title: "Wasp",
    firstname: "Janet",
    lastname: "Van Dyne",
    movies: [
      { title: "Ant-Man", year: 2015 },
      { title: "Ant‑Man and the Wasp", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Scarlet Witch",
    firstname: "Wanda",
    lastname: "Maximoff",
    movies: [
      { title: "Captain America: The Winter Soldier", year: 2014 },
      { title: "Avengers: Age of Ultron", year: 2015 },
      { title: "Captain America: Civil War", year: 2016 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
      { title: "Doctor Strange in the Multiverse of Madness", year: 2022 },
    ],
  },
  {
    title: "Black Widow",
    firstname: "Natasha",
    lastname: "Romanoff",
    movies: [
      { title: "Iron Man 2", year: 2010 },
      { title: "Avengers", year: 2012 },
      { title: "Captain America: The Winter Soldier", year: 2014 },
      { title: "Avengers: Age of Ultron", year: 2015 },
      { title: "Captain America: Civil War", year: 2016 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Captain Marvel",
    firstname: "Carol",
    lastname: "Danvers",
    movies: [
      { title: "Captain Marvel", year: 2019 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Gamora",
    firstname: "Gamora Zen",
    lastname: "Whoberi Ben Titan",
    movies: [
      { title: "Guardians of the Galaxy", year: 2014 },
      { title: "Guardians of the Galaxy Vol. 2", year: 2017 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
    ],
  },
  {
    title: "Shuri",
    firstname: "Shuri",
    lastname: "Princess",
    movies: [
      { title: "Black Panther", year: 2018 },
      { title: "Avengers: Infinity War", year: 2018 },
      { title: "Avengers: Endgame", year: 2019 },
      { title: "Black Panther: Wakanda Forever", year: 2022 },
    ],
  },
]);

let avengers = computed(() => {
  const txtVal = searchTxt.value.toLowerCase();
  console.log(txtVal);

  // return ladyAvengers.value.filter(character => {
  //     character.firstname.toLowerCase().includes(searchTxt.value.toLowerCase());
  //     // console.log(ladyAvengers);
  // })

  return ladyAvengers.value.filter((nm) => {
    let movieTitle = nm.movies.map((movie) => movie.title);
    return (
      nm.title.toLowerCase().includes(txtVal) ||
      nm.firstname.toLowerCase().includes(txtVal) ||
      nm.lastname.toLowerCase().includes(txtVal) ||
      movieTitle.some((title) => title.toLowerCase().includes(txtVal))
    );
  });
});
</script>

<template>
  <div class="container">
    <h2>Avengers Filtering data</h2>
    <label>Search </label>
    <input type="text" v-model="searchTxt" />

    <ul>
      <li v-for="name in avengers" :key="name.title">
       Title -> {{ name.title }} <hr /> Firstname -> {{ name.firstname }} <hr />
        Lastname ->  {{ name.lastname }} <hr />
        <ul>
          <li v-for="movie in name.movies" :key="movie.title">
            {{ movie.title }} ({{ movie.year }})
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.container {
  font-family: sans-serif;
  max-width: 800px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid whitesmoke;
  border-radius: 8px;
  background-color: black;
}

h2 {
  color: white;
  text-align: center;
  margin-bottom: 20px;
}

label {
  display: inline-block;
  margin-right: 10px;
  font-weight: bold;
  color: white;
  margin-bottom: 20px;
}

input[type="text"] {
  padding: 10px;
  border: 1px solid white;
  border-radius: 4px;
  width: 100%;
  margin-bottom: 20px;
  box-sizing: border-box;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  background-color: white;
  border: 1px solid white;
  border-radius: 4px;
  padding: 15px;
  margin-bottom: 10px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
}

li strong {
  font-weight: bold;
  color: black;
}
</style>
