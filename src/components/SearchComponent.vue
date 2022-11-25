<script>
export default {
  name: "SearchComponent",
  data() {
    return {
      search: "",
      shows: [],
    };
  },
  methods: {
    async fetchShows() {
      console.log("fetching shows");
      const response = await fetch(
        `https://api.tvmaze.com/search/shows?q=${this.search}`
      );
      const shows = await response.json();
      this.shows = shows;
    },
    setLocalShowId(id) {
      console.log("setting local show id");
      localStorage.setItem("showId", id);
    },
    clearSearch() {
      this.search = "";
      this.shows = [];
    },
  },
};
</script>
<template>
  <div>
    <div class="flex w-full items-center">
      <div class="w-[80%]">
        <input
          type="text"
          placeholder="Search"
          class="input max-w-xs bg-base-100 w-full"
          @keyup="fetchShows"
          v-model="search"
        />
      </div>
      <div class="w-[20%] justify-center items-center" @click="clearSearch">
        <div>
          <svg width="32" height="32" viewBox="0 0 2048 2048">
            <path
              fill="#c5c9e2"
              d="m1115 1024l690 691l-90 90l-691-690l-691 690l-90-90l690-691l-690-691l90-90l691 690l691-690l90 90l-690 691z"
            />
          </svg>
        </div>
      </div>
    </div>
  </div>

  <div class="shows-searched h-80% overflow-y-scroll">
    <div
      v-for="show in shows"
      :key="show.show.id"
      class="show-searched flex items-center gap-4 py-4"
      @click="setLocalShowId(show.show.id)"
    >
      <div class="show-searched-image">
        <img
          v-if="show.show.image && show.show.image.medium"
          class="w-16 h-16 object-cover"
          :src="show.show.image.medium"
          @click="setLocalShowId(show.show.id)"
          alt=""
        />
      </div>
      <div class="show-searched-title">
        <h3 class="text-lg font-bold">{{ show.show.name }}</h3>
      </div>
    </div>
  </div>
</template>
