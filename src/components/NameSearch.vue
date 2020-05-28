<template>
  <div class="name-searcher">
    <input class="nameField" type="text" v-model="personName" placeholder="Ex: Mateus">
    <input class="searchButton" type="button" value="PESQUISAR" v-on:click="getNameQuantity">
    <div class="message">
      <p v-if="nameQuantity >= 1">No periodo de 1930 à 2010 existem {{ nameQuantity }} pessoas registradas no IBGE com o nome {{personName}}.</p>
      <p v-if="nameQuantity == null">Não existe registro no IBGE com o nome {{personName}}.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NameSearch',
  data() {
    return {
      nameQuantity: 0,
      personName: ''
    }
  },
  methods: {
    getNameQuantity(name){
      name = this.personName
      let totalNames;
      let url = `https://servicodados.ibge.gov.br/api/v2/censos/nomes/${name}`;

      fetch(url).then(response => {
        response.json()
        .then(parsedJson => {
          console.log(parsedJson)
          if (parsedJson.length >= 1) {
            let frequencyArray = parsedJson[0].res;
            let reducer = (accumulator, currentValue) => accumulator + currentValue.frequencia;
            totalNames = frequencyArray.reduce(reducer, 0);
            this.nameQuantity = totalNames;
          } else {
            this.nameQuantity = null;
          }
        })
      })
    }
  }
}
</script>

<style scoped>
  .nameField {
    width: 15%;
    height: 40px;
  }

  .searchButton {
    width: 8%;
    height: 50px;
    background: #2c3e50;
    border: none;
    border-radius: 4px;
    font-weight: 600;
    font-size: 13.33px;
    line-height: 36px;
    letter-spacing: 0.02em;
    color: #ffffff;
    font-family: "Poppins", sans-serif;
    cursor: pointer;
    margin-bottom: 16px;
    margin-left: 20px;
  }


</style>