<template>
  <div class="hello">
    <h1>{{ text }}</h1>
    <input type="button" value="Click Me!" @click.prevent="setRandomWordPair" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import eAdjectives from './e-adjectives';
import tNouns from './t-nouns';
import eNouns from './e-nouns';

const ies = "ies";
const es = "es";
const ves = "ves";
const endings: any = {
  y: ies,
  s: es,
  ss: es,
  sh: es,
  ch: es,
  x: es,
  z: es,
  f: ves,
  fe: ves,
};

export default defineComponent({
  name: 'vETGenerator',
  props: {
    msg: String,
  },
  data() {
    return {
      text: "",
    };
  },
  methods: {
    randomWordPair(): string {
      const eNoun = true && Math.random() < 0.5;
      const plural = !eNoun && Math.random() < 0.5;
      const randomE = Math.random();
      const randomT = Math.random();
      // console.log(randomE, randomT, eAdjectives, randomT, eNouns, tNouns);
      var e: string = eNoun
        ? eNouns[Math.round(randomT * eNouns.length)]
        : eAdjectives[Math.round(randomE * eAdjectives.length)];
      var t: string = tNouns[Math.round(randomT * tNouns.length)];

      if (plural) {
        var found = false;
        for (let chars = 0; chars < t.length; chars++) {
          const element = t.substring(t.length - chars, t.length);
          // console.log(endings[element], element, t.charAt(t.length - 2));
          if (endings[element]) {
            if (t.charAt(t.length - 1) == "y"
              && !["a", "e", "i", "o", "u"].includes(t.charAt(t.length - 2))) {
              t = t.substring(0, t.length - chars) + endings[element];
              found = true;
            }
            else break;
          }
        }

        if (!found)
          t = t + "s";
      }

      return `${e} ${t}`.toLocaleLowerCase();
    },
    setRandomWordPair() {
      //@ts-ignore
      this.text = this.randomWordPair();
    }
  },
  mounted() {
    this.setRandomWordPair();
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>