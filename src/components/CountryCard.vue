<template>
  <div class="card">
    <div class="card-header">
      <p class="card-title">
        {{ name }}
      </p>
    </div>
    <div className="card-footer">
      <div className="card-likes">
        <span className="card-category"
          >Capital: <strong>{{ capital }}</strong></span
        >
        <p>
          <strong>{{ population }} hab</strong>
        </p>
      </div>
      <div class="card-borders">
        <span class="card-border" v-for="border in borders" :key="border">{{
          border
        }}</span>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class CountryCard extends Vue {
  @Prop(String) readonly name: string;
  @Prop(String) readonly capital: string;
  @Prop(Number) readonly population: number;
  @Prop([]) readonly borders: number[];
}
</script>

<style scoped>
.card {
  display: flex;
  cursor: pointer;
  flex-direction: column;
  border: 1px solid black;
  width: 20em;
  height: 220px;
  border-radius: 5px;
  box-shadow: 2px 4px 4px;
  padding: 10px;
  margin-top: 15px;
  margin-left: 15px;
  background-color: aqua;
}

.card-header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.card-footer {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.card-close-button {
  color: red;
}
.card-title {
  font-weight: bold;
  display: block;
  text-align: left;
}

.card-likes {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.card-likes > span {
  margin-left: 10px;
  vertical-align: baseline;
}
.card-borders {
  display: flex;
  flex-wrap: wrap;
}
.card-border {
  border-radius: 5px;
  font-weight: bold;
  color: white;
  background-color: darkcyan;
  margin-left: 3px;
  padding: 5px;
}
</style>
