<template>
  <div class="wrapper">
    <div class="title">
      <h1 style="font-size: 2rem; font-weight: bold;">The XKCD Poster</h1>
    </div>

    <div class="content">
      <div class="menu">
        <h4>Characters</h4>
        <select v-model="character" >
          <option v-for="c of characters" :key="c.value" :value="c">{{
            c.label
          }}</option>
        </select>

        <h4>Name</h4>
        <input v-model="name" type="text" />

        <h4>Size (cm)</h4>
        <input v-model="size_input" type="number" min="25" max="50"/>

        <h4>Date Picker</h4>
        <input v-model="date" type="date" />
      </div>

      <div class="picture">
        <div class="frame">
          <div class="poster">
            <img
              alt="Choose your picture!"
              :src="character.src"
              :height="resize(size)"
            />
            <h4>{{ name }}</h4>
            <h4>{{ date }}</h4>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "picture",
  data() {
    return {
      characters: [
        { label: "Beret", value: 1, src: require("./assets/beret.png") },
        { label: "Ponytail", value: 2, src: require("./assets/ponytail.png") },
        { label: "Blackhat", value: 3, src: require("./assets/black_hat.png") },
        { label: "Cueball", value: 4, src: require("./assets/cueball.png") },
        { label: "Danish", value: 5, src: require("./assets/danish.png") },
        { label: "Hairy", value: 6, src: require("./assets/hairy.png") },
        { label: "Megan", value: 7, src: require("./assets/megan.png") }
      ],
      character: "",
      size: 40,
      size_input: 40,
      name: "",
      date: "",
    };
  },
  watch: {
    size_input(size){
      if(size<25){
        this.size=25;
      }else if(size>50){
        this.size=50;
      }else{
        this.size = size; 
      }
    }
  },
  methods: {
    resize(heightincm) {
      var heightinpx = (heightincm / 70) * 490;
      return heightinpx; 
    }
  }
};
</script>

<style>

* #app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

* {
  font-family: xkcd;
  font-size: 1.2rem; 
}

.wrapper {
  display: flex; 
  flex-direction: column; 
  margin: 0 auto; 
}

.title {
  text-align: center;
}

.content {
  display: flex;
  flex-direction: row;
  justify-content: center; 
  align-items: stretch; 
  flex-wrap: wrap; 
}

.menu {
  text-align: center; 
  padding-bottom: 50px;
}

input,
button,
select,
optgroup,
textarea {
  margin: 0;
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
  width: 80%;
  background-color: white;
  color: black;
  border: 2px solid;
  height: 3rem;
  text-align: center;
}

input,
button,
select,
optgroup,
textarea {
  margin: 0;
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
  height: 3rem;
  width: 80%;
  border-radius: 7px;
  text-align: center;
  color: black;
  border: 2px solid;
}

.picture {
  text-align: center;
  text-overflow: hidden;
  align-self: center; 
}

.frame {
  text-align: center;
  height: 490px;
  width: 350px;
  margin: auto;
  border-style: outset;
  display: flex; 
  justify-content: center;
  align-items: center;
}


h1 {
  margin-bottom: 2rem;
  
}

h4 {
  margin-top: 1rem;
  margin-bottom: 1rem;
  
}
</style>
