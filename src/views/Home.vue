<template>
  <div class="home">
    <div class="title">
      <h1>Random Gif Cat</h1>
    </div>

    <div class="select">
      <div class="label">
        <label>Título:</label>
        <label>Filtro:</label>
        <label>Color:</label>
        <label>Tamaño:</label>
      </div>
      <div class="input-select">
        <input v-model="title" class="titulo--input" type="text" />
        <select v-model="filterSelected" class="filtro--select">
          <option disabled selected>Seleccione:</option>
          <option
            @click="filterSelected = item"
            v-for="item in filter"
            :key="item.id"
            :value="item"
          >
            {{ item }}
          </option>
        </select>
        <div class="select_color">
          <select class="color--select" v-model="colorSelected">
            <option disabled selected>Seleccione:</option>
            <option
              @click="colorSelected = item"
              v-for="item in colors"
              :key="item.id"
              :value="item"
            >
              {{ item }}
            </option>
          </select>
          <div
            :style="{ 'background-color': this.colorSelected }"
            class="color-circle"
          ></div>
        </div>
        <input
          v-model.number="size"
          class="tamaño--input"
          type="number"
          min="1"
        />
      </div>
    </div>

    <div class="gif">
      <button @click="getCat">Obtener mi gatito</button>
      <div class="img-gif">
        <img v-if="imgSrc" :src="imgSrc" alt="Gatito" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      title: "",
      filter: ["blur", "mono", "sepia", "negative", "paint", "pixel"],
      colors: ["red", "green", "yellow", "blue", "black", "gray"],
      size: null,
      colorSelected: "Seleccione:",
      filterSelected: "Seleccione:",
      imgSrc: ""
    };
  },
  methods: {
    getCat() {
      this.imgSrc = `https://cataas.com/cat/gif/says/${this.title}?filter=${this.filterSelected}&color=${this.colorSelected}&size=${this.size}`;
    }
  }
};
</script>

<style lang="scss">
$bg-color-select: #f08080;
$bg-color-page: #add8e6;
body {
  padding: 0;
  margin: 0;
}
.home {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr 2fr 3fr;
  background-color: $bg-color-page;
}
.title,
.select,
.gif {
  display: flex;
  flex-flow: column wrap;
  justify-content: center;
  text-align: center;
}
.title {
  margin: 3rem 0 1rem;
  h1 {
    font-size: 2.5rem;
  }
}
.select {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: 100%;
  background-color: $bg-color-select;
  padding-right: 15rem;
  .label,
  .input-select {
    display: flex;
    flex-flow: column wrap;
    justify-content: center;
  }
  .label {
    align-content: flex-end;
    label {
      margin: 12px;
      text-align: right;
      font-size: 1.4rem;
    }
  }
  .select_color {
    display: flex;
    flex-flow: row wrap;
    justify-content: space-between;
    align-content: center;
    .color--select {
      width: 50%;
    }
    .color-circle {
      width: 25px;
      height: 25px;
      border-radius: 50%;
      margin: 10px;
    }
  }
  .input-select {
    align-content: flex-start;
    input,
    select {
      margin: 10px;
      font-size: 1.3rem;
    }
  }
}
.gif {
  justify-content: start;
  padding: 2rem 30%;
  button {
    line-height: 2;
    font-size: 1.25rem;
    border-radius: 5px;
    margin-bottom: 2rem;
  }
}
</style>
