<template>
  <div class="poke-image">
    <!-- Affichage de l'image -->
    <img :src="infoPokemonImage" alt />
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      id: "", //Variable qui stock l'id du pokémon
      infoPokemonImage: "" //Variable qui stock l'image du pokemon
    };
  },
  mounted: function() {
    this.id = window.location.href;
    this.id = this.id.split("/");
    this.id = this.id[this.id.length - 1];
    this.id = Number(this.id);
    //Requête axios nous permettant de réccupérer l'image du pokémon
    axios.get(`https://pokeapi.co/api/v2/pokemon/${this.id}`).then(result => {
      if (result.status != 200) {
        window.location.replace("error.php");
      }
      //Affectation de l'image a la variable infoPokemonImage
      this.infoPokemonImage = result.data.sprites.front_default;
    });
  }
};
</script>

<style lang="css" scoped>
.poke-image {
  background: #e7e7e7;
  border-radius: 20px;
  display: flex;
  align-items: center;
}

.poke-image img {
  width: 100%;
  background: #e7e7e7;
  border-radius: 20px;
}
</style>
