<template>
    <div class="container">
       <div class="row">
        <div class="col-12 mb-4">
            <h1 class="title">Clique em duas imagens pra mudá-las de lugar</h1>
            <div class="game-set my-3">
              <button @click="start" id="start-button">Iniciar o Jogo</button>
              <button @click="stop" id="quit-button">Desistir</button>
            </div>
            <p>Tempo Decorrido: {{ elapsedTime }}</p>
            <p v-if="isWinning">Você Venceu!</p>
            <div class="row">
              <div
                class="column"
                v-for="(s, index) of shuffledPuzzleArray"
                :key="s"
                @click="swap(index)"
              >
                <img :src="require(`../assets/${puzzleId}/${s}`)" />
              </div>
            </div>
        </div>
      </div>
    </div>
</template>

<script>
import moment from "moment";

const correctPuzzleArray = [
  "image_part_001.jpg",
  "image_part_002.jpg",
  "image_part_003.jpg",
  "image_part_004.jpg",
  "image_part_005.jpg",
  "image_part_006.jpg",
  "image_part_007.jpg",
  "image_part_008.jpg",
  "image_part_009.jpg",
];

export default {
  name: "SliderPuzzle",
  props: {
    puzzleId: {
      type: String,
      default: "cut-pink",
    },
  },
  data() {  //data method. retorna um objeto
    return {
      correctPuzzleArray,
      shuffledPuzzleArray: [...correctPuzzleArray].sort(
        () => Math.random() - 0.5
      ), //usa spread operator ... para copiar correctPuzzleArray
      indexesToSwap: [],
      timer: undefined,
      startDateTime: new Date(),
      currentDateTime: new Date(),
    };
  },
  computed: { //computed property. contém o state/estado do game
    isWinning() {
      for (let i = 0; i < correctPuzzleArray.length; i++) {
        if (correctPuzzleArray[i] !== this.shuffledPuzzleArray[i]) {
          return false;
        }
      }
      return true;
    },
    elapsedDiff() {
      const currentDateTime = moment(this.currentDateTime);
      const startDateTime = moment(this.startDateTime);
      return currentDateTime.diff(startDateTime);
    },
    elapsedTime() {
      return moment.utc(this.elapsedDiff).format("HH:mm:ss");
    },
  },
  methods: {
    swap(index) {
      if (!this.timer) {
        return;
      }
      if (this.indexesToSwap.length < 2) {
        this.indexesToSwap.push(index);
      }
      if (this.indexesToSwap.length === 2) {
        const [index1, index2] = this.indexesToSwap;
        [this.shuffledPuzzleArray[index1], this.shuffledPuzzleArray[index2]] = [
          this.shuffledPuzzleArray[index2],
          this.shuffledPuzzleArray[index1],
        ];
        this.indexesToSwap = [];
      }
    },
    start() {
      this.resetTime();
      this.shuffledPuzzleArray = [...correctPuzzleArray].sort(
        () => Math.random() - 0.5
      );
      this.indexesToSwap = [];
      this.timer = setInterval(() => {      //callback function, tempo de intervalo entre cada chamada da callback
        this.currentDateTime = new Date();
        if (this.isWinning) {
          this.recordSpeedRecords();
          this.stop();
        }
      }, 1000);
    },
    stop() {
      this.resetTime();
      clearInterval(this.timer);
    },
    resetTime() {
      this.startDateTime = new Date();
      this.currentDateTime = new Date();
    },
    recordSpeedRecords() {
      let records = JSON.parse(localStorage.getItem("records")) || [];
      const { elapsedTime, elapsedDiff } = this;
      records.push({ elapsedTime, elapsedDiff });
      const sortedRecords = records
        .sort((a, b) => a.elapsedDiff - b.elapsedDiff)
        .slice(0, 10);
      const stringifiedRecords = JSON.stringify(sortedRecords);
      localStorage.setItem("records", stringifiedRecords);
    },
  },
};
</script>

<style scoped>
.row {
  display: flex;
  max-width: 90vw;
  flex-wrap: wrap;
}

.column {
  flex-grow: 1;
  width: 33%;
}

.column img {
  max-width: 100%;
}

.game-set {
  display: flex;
}

.game-set button {
  margin-right: 10px;
}

button {
  border: 1px solid #9f0c88;
  border-radius: 2px;
  font-family: "Open Sans",sans-serif;
  font-weight: 600;
  font-size: 12px;
  color: #ffffff;
  background: #9f0c88;
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
}
</style>
