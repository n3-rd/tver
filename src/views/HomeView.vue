<script>
import ShowTitle from "../components/ShowTitle.vue";
import ShowImage from "../components/ShowImage.vue";

export default {
  components: {
    ShowTitle,
    ShowImage,
  },
  data() {
    return {
      show: [],
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
  },
  mounted() {
    this.populateLocalShowId();
    this.refreshShow();
    this.fetchShow();
    setInterval(() => {
      this.refreshShow();
      this.fetchShow();
    }, 1000);
  },
};
</script>

<template>
  <main>
    <div class="w-full flex h-screen items-center px-6">
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
  </main>
</template>
