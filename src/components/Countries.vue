<template>
  <div class="countries">
    <h1>Countries</h1>
    <p>Average population of selected countries: {{ averagePopulation }}</p>
    <ul v-for="country in queryCountry" :key="country.name">
      <li v-on:click="onCountryClick(country)">
        <CountryCard
          :name="country.name"
          :population="country.population"
          :capital="country.capital"
        />
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { countries$, Country } from "../services/FetchCountries";
import { Component, Prop, Vue, Watch } from "vue-property-decorator";
import { sortBy } from "lodash";
import CountryCard from "./CountryCard.vue";

@Component({
  components: {
    CountryCard
  }
})
export default class Countries extends Vue {
  @Prop(String) readonly sort: string = "One";

  @Prop(String) readonly query: string = "";
  private countries: Country[] = [];

  mounted() {
    this.getCountries();
  }
  get queryCountry() {
    let sorted: Country[];
    if (this.sort === "Two") {
      sorted = sortBy(this.countries, country => country.population);
    } else {
      sorted = this.countries;
    }
    return this.query.length
      ? sorted.filter(({ name }) =>
          name.toLowerCase().startsWith(this.query.toLowerCase())
        )
      : [];
  }

  get averagePopulation() {
    //  console.log("averagePopulation", this.queryCountry);
    // console.log("averagePopulation", this.queryCountry.length);
    return (
      this.queryCountry.reduce((sum, { population }) => sum + population, 0) /
        this.queryCountry.length || 0
    );
  }
  @Watch("queryCountry")
  async listChanged(newVal: Country[]) {
    //console.log("yeah latlngSelectdCountry Countries");
    this.$emit("selected-country-latlng", {
      latlngs: newVal.map(({ latlng }) => latlng)
    });
  }

  onCountryClick(country: Country) {
    // console.log("country", country.latlng);
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
