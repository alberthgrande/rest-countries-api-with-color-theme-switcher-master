<template>
  <div class="container mx-auto">
    <NavBar />
    <div class="my-6">
      <input
        class="w-full max-w-md px-4 py-2 border rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
        type="text"
        v-model="searchCountry"
        placeholder="Search for a country..."
      />
    </div>
    <div
      class="grid grid-cols-1 gap-16 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 place-content-center"
    >
      <div
        v-for="country in filteredCountry"
        :key="country.id"
        class="rounded-lg shadow-md overflow-hidden"
      >
        <div>
          <img
            class="w-full h-48 object-cover"
            :src="country.flags.svg"
            :alt="country.name"
          />
        </div>
        <div class="p-8">
          <h3 class="text-lg font-semibold">{{ country.name }}</h3>
          <p class="mt-2">
            <strong>Population:</strong>
            {{ country.population.toLocaleString() }}
          </p>
          <p><strong>Region:</strong> {{ country.region }}</p>
          <p>
            <strong>Capital:</strong>
            {{ country.capital ? country.capital : "N/A" }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import userData from "./assets/data.json";
import NavBar from "./components/NavBar.vue";

export default {
  components: {
    NavBar,
  },
  data() {
    return {
      countries: userData,
      searchCountry: "",
    };
  },
  computed: {
    filteredCountry() {
      return this.countries.filter((country) => {
        return country.name
          .toLowerCase()
          .includes(this.searchCountry.toLowerCase());
      });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
