<template>
  <div class="card">
    <div class="header">
      {{ movie.title }}
    </div>
    <div class="card-body ">
      <img :src="movie.posterurl" width="95" height="110" alt="" onerror="this.src='https://www.media4.hw-static.com/media/2015/12/fright-night-columbia-pictures-everett-122315.jpg'" />
      <div class="mh-48">
        <div class="ml-2 ">
          <div class="badge badge-success inline-block">Available</div>
          <div v-if="listType == 'list'">
            <span class="font-medium">Actors: </span>
            {{ movie.actors.join(", ") }}
          </div>
          <div class="overflow-ellipsis">
            {{ trimStory(movie.storyline) }}
          </div>
          <div class="badge-info badge inline-block">{{ movie.genres.join(", ") }}</div>
        </div>
      </div>
    </div>
    <div class="footer mt-2 flex justify-between">
      <div class="flex py-1">
        <div class="flex items-center ">
          <svg
            v-for="start in 5"
            :key="start"
            class="mx-1 w-4 h-4 fill-current "
            :class="[rating(movie.imdbRating) >= start ? 'text-yellow-500' : 'text-gray-400']"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 20 20"
          >
            <path d="M10 15l-5.878 3.09 1.123-6.545L.489 6.91l6.572-.955L10 0l2.939 5.955 6.572.955-4.756 4.635 1.123 6.545z" />
          </svg>
        </div>
      </div>
      <div class="flex mr-3 text-blue-700">
        <div class="mr-1">Trailer</div>
        <div>
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mt-1" viewBox="0 0 20 20" fill="currentColor">
            <path d="M2 6a2 2 0 012-2h6a2 2 0 012 2v8a2 2 0 01-2 2H4a2 2 0 01-2-2V6zM14.553 7.106A1 1 0 0014 8v4a1 1 0 00.553.894l2 1A1 1 0 0018 13V7a1 1 0 00-1.447-.894l-2 1z" />
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    movie: Object,
    listType: String,
  },
  computed: {
    maxStroyLength() {
      return this.listType == "grid" ? 130 : 600;
    },
  },
  methods: {
    trimStory(title) {
      if (title.length >= this.maxStroyLength) {
        return title.substring(0, this.maxStroyLength) + "...";
      }
      return title;
    },
    rating(rating) {
      return Math.round(rating / 2);
    },
  },
};
</script>
<style lang="scss" scoped>
.card {
  @apply border-gray-300 border  rounded-md m-3;
  & > div {
    @apply pl-3;
  }
  .header {
    @apply py-3  bg-gray-200 text-base font-medium;
  }
  .card-body {
    @apply pt-3 flex;

    img {
      // width: 83px;
      // height: 122px;
    }
  }
  .footer {
    @apply py-3  bg-gray-200 text-base;
  }
}
.badge {
  padding: 1px 5px;
  font-size: 0.75rem;
  line-height: 1rem;
  border-radius: 0.125rem;
  font-weight: 600;
}

.badge-success {
  color: white;
  background-color: #40a939;
}
.badge-info {
  @apply bg-blue-500 text-white;
}
.mh-48 {
  min-height: 150px;
}
</style>
