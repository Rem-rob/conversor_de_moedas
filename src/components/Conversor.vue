<template>
  <div class="conversor">
    <h2>{{ moedaA }} Para {{ moedaB }}</h2>
    <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA" />
    <input type="button" value="Converter" v-on:click="converter">
    <h2>{{ moedaB_value }}</h2>
  </div>
</template>

<script>
export default {
  name: "Conversor",
  props: ["moedaA", "moedaB"],
  data() {
    return {
      moedaA_value: "",
      moedaB_value: 0,
    };
  },

  methods: {
    converter() {
      let de_para = this.moedaA + "_" + this.moedaB;
      let url =
        "https://free.currconv.com/api/v7/convert?q=" +
        de_para +
        "&compact=ultra&apiKey=854cfa26c8d0a2f2a859";

      fetch(url).then(res=>{return res.json()})
        .then(json => {
            let cotacao = json[de_para];
            this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(
                2
                );
        });
    }
  }
};
</script>

<style scoped>

.conversor{
    padding: 20px;
    max-width: 300px;
    box-shadow: 0 4px 8px rgb(0, 0,0, 0.2);

}

</style>