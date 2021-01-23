<template>
  <div>
    <div class="h-16 w-full bg-blue-900">
      <div class="grid grid-cols-1 md:grid-cols-3 grid-flow-col px-5">
        <div>
          <div class="h-5 mt-3">
            <div class="flex">
              <input class="rounded-l-lg p-2 bg-white w-full" placeholder="Search Movies" v-model="searchQuery" />
              <button class="px-5 rounded-r-lg bg-yellow-400 p-3">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                </svg>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="hidden md:block">
      <div class="flex justify-end mx-3 my-2 gap-2">
        <button @click="listType = 'grid'">
          <svg xmlns="http://www.w3.org/2000/svg" class="rounded w-8 h-7 text-white" :class="[listType == 'grid' ? ' bg-yellow-500' : 'bg-gray-500']" viewBox="0 0 20 20" fill="currentColor">
            <path
              d="M5 3a2 2 0 00-2 2v2a2 2 0 002 2h2a2 2 0 002-2V5a2 2 0 00-2-2H5zM5 11a2 2 0 00-2 2v2a2 2 0 002 2h2a2 2 0 002-2v-2a2 2 0 00-2-2H5zM11 5a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V5zM11 13a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z"
            />
          </svg>
        </button>
        <button @click="listType = 'list'">
          <svg xmlns="http://www.w3.org/2000/svg" class="rounded w-8 h-7  text-white" :class="[listType == 'list' ? ' bg-yellow-500' : 'bg-gray-500']" viewBox="0 0 20 20" fill="currentColor">
            <path
              fill-rule="evenodd"
              d="M3 4a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm0 4a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm0 4a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm0 4a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z"
              clip-rule="evenodd"
            />
          </svg>
        </button>
      </div>
    </div>
    <div class="grid grid-cols-1  gap-1" :class="{ 'md:grid-cols-3': listType == 'grid' }">
      <MovieCard :movie="movie" v-for="movie in moviesList" :key="movie.id" :list-type="listType" />
    </div>
  </div>
</template>

<script>
import movies from "@/movies.json";
import MovieCard from "@/components/Movie.vue";
export default {
  name: "Home",
  components: { MovieCard },
  data() {
    return {
      movies: movies,
      listType: "grid",
      searchQuery: "",
    };
  },
  methods: {},
  computed: {
    moviesList() {
      if (this.searchQuery) {
        return this.movies.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => item.title.toLowerCase().includes(v));
        });
      } else {
        return this.movies;
      }
    },
  },
};
</script>
