<template>
  <div>
    <h1 class="puzzle-title">Escolha um quebra-cabeça</h1>
    <div v-for="p of puzzles" :key="p.id" class="row">
      <div class="puzzle-thumbnail">
        <img :src="require(`../assets/${p.image}`)" />
      </div>
      <div>
        <h2>{{p.title}}</h2>
      </div>
      <div class="play-button">
        <button @click="selectPuzzle(p)">Jogar</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      puzzles: [
        { id: 'cut-pink', image: "pink.jpg", title: "Flor Rosa" },
        { id: 'cut-purple', image: "purple.jpg", title: "Flor Roxa" },
        { id: 'cut-red', image: "red.jpg", title: "Flor Vermelha" },
      ],
    };
  },
  methods: {
    selectPuzzle(puzzle){
      this.$emit('puzzle-changed', puzzle.id); //(name, id)emit the event to parent component app.vue. Lido no parent com v-on
    }
  }
};
</script>

<style scoped>
.row {
  display: flex;
  max-width: 90vw;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
}

.row img {
  width: 100px;
}

.row .play-button {
  padding-top: 25px;
}

.puzzle-title {
  font-family: "Open Sans",sans-serif;
  font-weight: 600;
  font-size: 48px;
  color: #111;
  letter-spacing: 1.34px;
  padding-bottom: 32px;
}

.puzzle-thumbnail {
  margin: 10px;
  border: 1px solid transparent;
  box-shadow: 0 4px 15px 0px rgb(0 0 0 / 10%);
}

.puzzle-thumbnail img {
  border-radius: 2px;
  box-shadow: 0 4px 15px 0px rgb(0 0 0 / 10%);
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
  width: 115px;
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
</style>
