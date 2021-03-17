<template>
  <div class="card" :class="{ flipped: isShown }">
    <div class="card-inner" @click="handleClick">
      <div class="back-side">
        <img src="@/assets/images/question-mark.png" alt="hidden card" />
      </div>
      <div class="language-side">
        <img
          :src="require('@/assets/images/' + language.image)"
          :alt="language.name"
          :title="language.name"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["language", "guess1", "guess2"],
  methods: {
    handleClick() {
      this.$emit("select", this.language);
    },
  },
  computed: {
    isShown() {
      return (
        this.language.foundMatch ||
        this.language === this.guess1 ||
        this.language === this.guess2
      );
    },
  },
};
</script>

<style scoped>
img {
  height: 100px;
}
.card {
  background-color: transparent;
  width: 100px;
  height: 100px;
  perspective: 1000px;
  margin-top: 20px;
}
.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}
.flipped .card-inner {
  transform: rotateY(180deg);
}
.back-side,
.language-side {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}
.back-side {
  background-color: goldenrod;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto 60px;
}
.language-side {
  background-color: goldenrod;
  color: black;
  transform: rotateY(180deg);
}
</style>