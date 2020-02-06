<template>
  <div id="app">
    <div class="progress">
      <div class="progressBar" :style="{width: quotes.length*10 + '%'}"></div>
      <span class="quoteCount">{{quotes.length}} / 10</span>
    </div>
    <div class="addQuote">
      <input type="text" v-model="quoteBox" placeholder="Add a quote" ref="quote">
      <br>
      <button
        class="button"
        :disabled="quoteBox.length ===0 || quotes.length === 10"
        @click="AddQuote()"
      >Add</button>
    </div>
    <div class="quotes">
      <quote @DeleteQuote="DeleteQuote" v-for="quote in quotes" :key="quote.id" :quoteId="quote.id">
        <h3 :id="quote.id">{{quote.quote}}</h3>
      </quote>
    </div>
  </div>
</template>

<script>
import quote from "@/components/quote";

export default {
  name: "App",
  components: { quote },
  data() {
    return {
      quotes: [],
      quoteBox: ""
    };
  },
  methods: {
    AddQuote() {
      let newID = Math.max(...this.quotes.map(quote => quote.id), 0) + 1;
      this.quotes.push({ id: newID, quote: this.quoteBox });
      this.quoteBox = "";
      console.log(this.$refs.quote.focus()); //.quote.$el.focus();
    },
    DeleteQuote(quoteId) {
      this.quotes.splice(
        this.quotes.findIndex(quote => quote.id === quoteId),
        1
      );
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>

<style scoped>
.progress {
  width: 80%;
  background-color: #CCC;
  position: relative;
  margin: 20px auto;
  padding: 10px;
  box-sizing: border-box;
  height: 36px;
}

input {
  width: 80%;
  padding: 5px;
  margin: 0;
  box-sizing: border-box;
}

button {
  padding: 5px 10px;
  color: #FFF;
  background-color: #0072bc;
  cursor: pointer;
  border: 1px solid #CCC;
  margin: 10px;
  display: inline-block;
}

button:disabled {
  background-color: #0072bc55;
}

.quotes {
  display: flex;
  align-content: start;

  flex-wrap: wrap;
}

/*.quotes::after {
  content: "";
  flex: auto;
}*/

.progressBar {
  background-color: green;
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  transition: width 0.2s ease-out;
}

.quoteCount {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
