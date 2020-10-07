<template>
  <div class="card">
    <h3>{{ name }}</h3>
    <p>{{ capital }}</p>
    <p>{{ population }}</p>
    <span v-for="border in borders" :key="border">{{ border }}</span>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class CountryCard extends Vue {
  @Prop(String) readonly name: string;
  @Prop(String) readonly capital;
  @Prop(Number) readonly population: number;
  @Prop([]) readonly borders: number[];
}
</script>

<style scoped>
li {
  cursor: pointer;
}
</style>
