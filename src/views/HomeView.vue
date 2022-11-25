<script>
import ShowTitle from "../components/ShowTitle.vue";
import ShowImage from "../components/ShowImage.vue";
import CastSection from "../components/CastSection.vue";

export default {
  components: {
    ShowTitle,
    ShowImage,
    CastSection,
  },
  data() {
    return {
      show: [],
      cast: [],
    };
  },
  methods: {
    async fetchShow() {
      const response = await fetch(
        `https://api.tvmaze.com/shows/${localStorage.getItem("showId")}`
      );
      const show = await response.json();
      this.show = show;
    },
    populateLocalShowId() {
      if (!localStorage.getItem("showId")) {
        localStorage.setItem("showId", 84);
      }
    },
    refreshShow() {
      localStorage.getItem("showId");
    },
    fetchCast() {
      fetch(
        `https://api.tvmaze.com/shows/${localStorage.getItem("showId")}/cast`
      )
        .then((response) => response.json())
        .then((cast) => {
          this.cast = cast;
        });
    },
  },
  mounted() {
    this.populateLocalShowId();
    this.refreshShow();
    this.fetchShow();
    this.fetchCast();
    setInterval(() => {
      this.refreshShow();
      this.fetchShow();
    }, 1000);
  },
};
</script>

<template>
  <main class="px-6">
    <div class="w-full flex h-screen items-center">
      <div class="show-title w-[50%]">
        <ShowTitle
          :title="show.name"
          :years="show.premiered"
          :summary="show.summary"
          :website="show.officialSite"
          :status="show.status"
          :ended="show.ended"
          :rating="show.rating.average"
          v-if="show.rating"
        />
      </div>
      <div class="show-image w-[50%] flex justify-center" v-if="show.image">
        <ShowImage class="show-image-inner" :imageSrc="show.image.original" />
      </div>
    </div>
    <div class="cast">
      <CastSection :cast="cast" />
    </div>
  </main>
</template>
