<template>
  <div :class="{ dark: isDark }" class="container mx-auto">
    <NavBar />
    <div class="my-6 flex flex-col md:flex-row justify-between gap-4 md:gap-6">
      <div>
        <input
          class="w-full max-w-md px-4 py-3 border rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
          type="text"
          v-model="searchCountry"
          placeholder="Search for a country..."
        />
      </div>
      <div>
        <select
          class="w-full max-w-md px-4 py-3 border rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
          v-model="selectedRegion"
        >
          <option value="">Filter by Region</option>
          <option v-for="region in regions" :key="region" :value="region">
            {{ region }}
          </option>
        </select>

        <p>Selected Region: {{ selectedRegion }}</p>
      </div>
    </div>

    <div
      class="grid grid-cols-1 gap-16 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 place-content-center"
    >
      <div
        v-for="country in filteredCountry"
        :key="country.id"
        class="grid-card rounded-lg shadow-md overflow-hidden"
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
import { useDark } from "@vueuse/core";

export default {
  components: {
    NavBar,
  },
  data() {
    return {
      countries: userData,
      searchCountry: "",
      selectedRegion: "",
      regions: ["Africa", "Asia", "Europe", "Oceania"],
    };
  },
  computed: {
    filteredCountry() {
      return this.countries.filter((country) => {
        const searchQuery = this.searchCountry.toLowerCase();
        const matchesSearch =
          (country.name && country.name.toLowerCase().includes(searchQuery)) ||
          (country.capital &&
            country.capital.toLowerCase().includes(searchQuery));

        const matchesRegion = this.selectedRegion
          ? country.region === this.selectedRegion
          : true; // If no region is selected, include all

        return matchesSearch && matchesRegion;
      });
    },
  },
  // computed: {
  //   filteredCountry() {
  //     return this.countries.filter((country) => {
  //       const searchQuery = this.searchCountry.toLowerCase();
  //       return (
  //         (country.name && country.name.toLowerCase().includes(searchQuery)) ||
  //         (country.capital &&
  //           country.capital.toLowerCase().includes(searchQuery))
  //       );
  //     });
  //   },
  // },
  setup() {
    const isDark = useDark(); // VueUse dark mode hook
    return { isDark };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

/* Dark mode styles */
.dark {
  background: #242424;
  color: #fff;
}

/* Light grid card styles */
.grid-card {
  background-color: #ffffff; /* Lighter background */
  color: #333; /* Dark text for contrast */
  border: 1px solid #ddd; /* Light border */
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* Soft shadow */
}

/* Dark mode grid card styles */
.dark .grid-card {
  background-color: #333; /* Dark background */
  color: #fff; /* Light text */
  border: 1px solid #555; /* Darker border */
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.4); /* Darker shadow */
}

/* Input field styling */
.dark input[type="text"] {
  background-color: #333;
  color: #fff;
  border-color: #555;
}

/* Regular light mode styles for input */
input[type="text"] {
  background-color: white;
  color: #333;
  border-color: #ddd;
}

/* Input field styling */
.dark select {
  background-color: #333;
  color: #fff;
  border-color: #555;
}

/* Regular light mode styles for input */
select {
  background-color: white;
  color: #333;
  border-color: #ddd;
}
</style>
