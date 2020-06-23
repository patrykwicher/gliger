<template>
<div id="app">
  <div id="box" v-on:click="boxClick()"></div>
  <div id="counter"> {{ counter.points }} </div>
  <div id="heroes-container">
    <div id="hero" v-for="hero in arrayOfHeroes" :key="hero.id" v-on:click="buyHero(hero)">
      <img class="faces" v-bind:src="hero.img" />
      <h2> {{hero.name}} </h2>
      <p> Price: {{hero.price}} </p>
      <p> Quantity: {{hero.quantity}} </p>
      <p> Cookies: {{hero.generatedCookies}} </p>
    </div>
  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      counter: {
        count: 0,
        get points() {
          return this.count;
        },
        set points(update) {
          this.count = update;
        },
      },
      arrayOfHeroes: [{
          id: 0,
          name: 'Ohydziarz',
          price: 5,
          quantity: 0,
          baseCookies: 1,
          generatedCookies: 0,
          img: 'https://minecraftfaces.com/wp-content/bigfaces/big-villager-face.png',
        },
        {
          id: 1,
          name: 'Feru',
          price: 40,
          quantity: 0,
          baseCookies: 8,
          generatedCookies: 0,
          img: 'https://i.pinimg.com/originals/07/b3/ac/07b3ac2fb39db7554a1badbc0c9d94a8.png',
        },
        {
          id: 2,
          name: 'Ambroży Zróbfikoła',
          price: 80,
          quantity: 0,
          baseCookies: 15,
          generatedCookies: 0,
          img: 'https://minecraftfaces.com/wp-content/bigfaces/big-enderman-face.png'
        },
      ],
      sum: 0,
    };
  },
  methods: {
    boxClick() {
      this.counter.points += 1;
    },
    buyHero(hero){
      let { id, price, baseCookies } = hero;
      if(price > this.counter.count) alert("za mało punktów");
      else {
        this.arrayOfHeroes[id].price += Math.floor(price - (price/2));
        this.arrayOfHeroes[id].quantity += 1;
        this.arrayOfHeroes[id].generatedCookies += baseCookies;
        this.counter.points -= price;
        this.sum += this.arrayOfHeroes[id].baseCookies;
      }
    },
    addToCounter() {
      this.counter.points += this.sum;
    },
  },
  mounted: function(){
    setInterval(this.addToCounter, 2000);
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');

#app {
  font-family: 'VT323', monospace;
  background-color: #f8f8ff;
}

#counter {
  text-align: center;
  font-size: 5em;
}

#heroes-container {
  display: grid;
  grid-template-columns: auto auto auto;
  text-align: center;
  border: 1px solid black;
  border-left: none;
  border-right: none;
}

#box {
  background-color: black;
  height: 7em;
  width: 7em;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 1em;
  border-radius: 50%;
}

#hero {
  padding: 5% 0 1% 0;
}

#hero img {
  width: 8em;
  height: auto;
}
</style>
