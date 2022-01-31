<template>
  <div>
    <Puzzles @puzzle-changed="selectedPuzzleId = $event" />
    <Records />
    <SliderPuzzle :puzzleId="selectedPuzzleId" />
  </div>
</template>

<script>
import SliderPuzzle from "./components/SliderPuzzle.vue";
import Puzzles from "./components/Puzzles.vue";
import Records from "./components/Records.vue";

export default {
  name: "App",
  components: {
    SliderPuzzle,
    Puzzles,
    Records,
  },
  data() {
    return {
      selectedPuzzleId: "cut-pink",
    };
  },
};
</script>

<style>

.title {
  font-family: "Open Sans",sans-serif;
  font-weight: 600;
  font-size: 2rem;
  color: #111;
  letter-spacing: 1.2px;
  padding-bottom: 32px;
}

h2 {
  font-family: "Open Sans",sans-serif;
  font-weight: 400;
  font-size: 25px;
  color: #111;
  letter-spacing: .58px;
}

button {
  border: 1px solid #9f0c88;
  border-radius: 2px;
  font-family: "Open Sans",sans-serif;
  font-weight: 600;
  font-size: 12px;
  color: #9f0c88;
  background: transparent;
  letter-spacing: .28px;
  text-align: center;
  min-width: 115px;
  height: 40px;
  line-height: 40px;
  display: block;
  text-transform: uppercase;
  transition: 200ms all;
  cursor: pointer;
}

button:hover {
  opacity: .8;
  transform: scale(1.02);
  background: #9f0c88;
  color: #fff;
}

button:focus {
  outline: none;
}

</style>
