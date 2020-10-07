<template>
  <div class="countries">
    <h1>Countries</h1>
    <ul v-for="country in queryCountry" :key="country.name">
      <li v-on:click="onCountryClick(country)">{{ country.name }}</li>
    </ul>
  </div>
</template>

<script lang="ts">
import { countries$, Country } from "../services/FetchCountries";
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Countries extends Vue {
  @Prop(String) readonly query: string = "";
  private countries: Country[] = [];

  mounted() {
    this.getCountries();
  }
  get queryCountry() {
    return this.query.length
      ? this.countries.filter(({ name }) =>
          name.toLowerCase().startsWith(this.query.toLowerCase())
        )
      : [];
  }
  onCountryClick(country: Country) {
    console.log("country", country.latlng);
    this.$emit("country-clicked", { latlng: country.latlng });
  }
  async getCountries() {
    const countries = await countries$;
    this.countries = countries;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
li {
  cursor: pointer;
}
</style>
