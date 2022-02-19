<template>
  <section
    class="home-intro-container items-center flex flex-col justify-center w-full text-center z-20 pt-32 pb-12"
    style="
      background-color: #1b58f4;
      background-image: url('https://img.alicdn.com/imgextra/i3/O1CN01OSBkaL1JL57ypRyZa_!!6000000001011-2-tps-2880-1400.png');
    "
  >
    <h1 class="font-normal font-serif text-display-5 mb-6 text-6xl text-white">
      Serverless Devs
    </h1>

    <h2 class="font-normal text-body-base text-2xl text-gray-200">
      {{ $t("home.intro") }}
    </h2>
    <div class="flex mt-12 mr-12">
      <el-button
        type="text"
        class="flex items-center border-inherit"
        style="color: #fff; padding: 0 1rem"
        @click="handlerStar"
      >
        <IconGithub class="w-4 h-4 text-white mr-1 inline-block -mt-1" />{{
          stars
        }}
        Github stars
      </el-button>
      <el-button class="ml-4" size="small" @click="handlerRouterStart">
        <NuxtLink :to="quickStart"> {{ $t("home.start") }} </NuxtLink>
      </el-button>
    </div>
  </section>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  data() {
    return {
      stars: 0,
      quickStart: "/serverless-devs/quick_start",
    };
  },
  computed: {
    ...mapGetters(["githubUrls"]),
    repo() {
      return this.githubUrls.api.repo;
    },
  },
  async mounted() {
    this.stars = localStorage.getItem("serverless_devs_star");
    try {
      const data = await fetch(this.repo)
        .then((res) => {
          if (!res.ok) {
            throw new Error(res.statusText);
          }
          return res;
        })
        .then((res) => res.json());
      this.stars = parseInt(data.stargazers_count, 10);
      localStorage.setItem("serverless_devs_star", this.stars);
    } catch (e) {}
  },
  methods: {
    handlerStar() {
      window.location.href =
        "https://github.com/Serverless-Devs/Serverless-Devs";
    },
    handlerRouterStart() {
      this.$router.push({ path: this.quickStart });
    },
  },
};
</script>
<style>
.home-intro-container .el-button--text {
  border-color: #f5f5f5;
}
.home-intro-container .el-button--text:hover {
  color: #f7fafc;
  color: rgba(247, 250, 252, var(--text-opacity));
  --bg-opacity: 1;
  background-color: #1b58f4;
  background-color: rgba(27, 88, 244, var(--bg-opacity));
}
</style>
