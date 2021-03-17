<template>
  <div>
    <h1>Find all the matches</h1>
    <div class="game-board">
      <div v-for="language in languages" :key="language.id" class="cell">
        <card
          :language="language"
          @select="handleCardClick"
          :guess1="guess1"
          :guess2="guess2"
        />
      </div>
    </div>
  </div>
</template>

<script>
import getLanguageCards from "../data";
import shuffle from "lodash.shuffle";
import Card from "./Card";

export default {
  components: { Card },
  data() {
    return {
      languages: shuffle(getLanguageCards()),
      guess1: null,
      guess2: null,
    };
  },
  methods: {
    handleCardClick(languageClicked) {
      // if there are two cards already flipped prevent a third from being flipped
      if (this.guess1 && this.guess2) return;
      // if the user clicked the same card twice don't do anything
      if (this.guess1 === languageClicked) return;
      if (this.guess1 === null) {
        this.guess1 = languageClicked;
        return;
      }
      this.guess2 = languageClicked;
      const [lang1, lang2] = this.getMatchingLangs(languageClicked.name);
      if (this.guess1.name === this.guess2.name) {
        lang1.foundMatch = true;
        lang2.foundMatch = true;
        this.guess1 = null;
        this.guess2 = null;
      } else {
        setTimeout(() => {
          // user made two wrong guesses. Wait 2 seconds and flip cards
          this.guess1 = null;
          this.guess2 = null;
        }, 1500);
      }
    },
    getMatchingLangs(name) {
      return this.languages.filter((l) => l.name === name);
    },
  },
  computed: {
    foundAllMatches() {
      return this.languages.every((l) => l.foundMatch);
    },
  },
};
</script>

<style scoped>
h1 {
  color: white;
}
.game-board {
  display: flex;
  flex-wrap: wrap;
  align-items: space-between;
  justify-content: center;
}
.cell {
  padding: 10px;
}
</style>