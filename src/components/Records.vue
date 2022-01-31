<template>
    <div class="container">
      <div class="row">
        <div class="col-12">
            <div class="mb-5">
              <h1 class="title">Records</h1>
              <div class="game-set my-3">
                <button @click="getRecords">Atualizar a Lista</button>
              </div>
              <div v-for="(r, index) of records" :key="index">{{index + 1}} - {{r.elapsedTime}}</div>
            </div>
        </div>
      </div>
    </div>

</template>

<script>
export default {
  data() {
    return {
      records: [],
    };
  },
  created() {
    this.getRecords();
  },
  methods: {
    getRecords() {
      const records = JSON.parse(localStorage.getItem("records")) || []; //parse the JSON string into an object
      this.records = records;
    },
  },
};
</script>

<style scoped>

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
