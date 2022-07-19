<template>
  <nav
    class="top-0 z-40 w-full border-b dark:border-gray-800 dark:bg-gray-900"
    :class="{ 'shadow border-transparent': scrolled, 'fixed' : !isHome || scrolled > 40 }"
    @click="scrollToTop"
    style="box-shadow: 0 1px 4px 0 rgb(0 21 41 / 12%); background-color: rgb(250 251 255)!important;"
  >
    <div class="container mx-auto flex-1">
      <div class="flex items-center justify-between h-16">
        <div class="w-max mr-8 flex items-center pr-4" @click.stop="noop">
          <a
            :href="settings.url"
            class="flex-shrink-0 flex-1 font-bold text-xl"
            :aria-label="`${settings.title} Logo`"
          >
            <span v-if="!logo">{{ settings.title }}</span>

            <img
              v-if="logo"
              :src="logo.light"
              class="h-12 max-w-full light-img"
              :alt="settings.title"
            />
            <img
              v-if="logo"
              :src="logo.dark"
              class="h-12 max-w-full dark-img"
              :alt="settings.title"
            />
          </a>
        </div>
        <div
          v-if="settings.layout !== 'single'"
          class="flex-1 flex justify-start w-4/6"
        >
          <AppSearchAlgolia
            v-if="settings.algolia"
            :options="settings.algolia"
            :settings="settings"
          />
          <AppSearch v-else class="hidden lg:block" />
        </div>
        <div
          class="flex items-center pl-4 lg:pl-8"
          :class="{
            'justify-between': lastRelease && settings.layout !== 'single',
            'justify-end': !lastRelease || settings.layout === 'single',
          }"
        >
          <div class="flex items-center">
            <HeaderLink />
            <AppLangSwitcher class="ml-4"/>
            <a
              v-if="settings.github"
              :href="githubUrls.repo"
              target="_blank"
              rel="noopener noreferrer"
              title="Github"
              name="Github"
              class="text-gray-700 dark:text-gray-300 hover:text-primary-500 dark-hover:text-primary-500 ml-4"
              :class="{
                'hidden lg:block': settings.layout !== 'single',
              }"
            >
              <IconGithub class="w-5 h-5" />
            </a>
            <button
              v-if="settings.layout !== 'single'"
              class="lg:hidden p-2 rounded-md text-gray-700 dark:text-gray-300 focus:outline-none -mr-2"
              aria-label="Menu"
              @click.stop="menu = !menu"
            >
              <IconX v-if="menu" class="w-5 h-5" />
              <IconMenu v-else class="w-5 h-5" />
            </button>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { mapGetters } from "vuex";
import { useNav } from "~/plugins/nav";
import HeaderLink from "./HeaderLink";
import { defineComponent } from "@nuxtjs/composition-api";

export default defineComponent({
  component: {
    HeaderLink,
  },
  setup() {
    const { isHome } = useNav();
    return {
      isHome,
    };
  },
  data() {
    return {
      scrolled: 0,
    };
  },
  computed: {
    ...mapGetters(["settings", "githubUrls", "lastRelease"]),
    menu: {
      get() {
        return this.$store.state.menu.open;
      },
      set(val) {
        this.$store.commit("menu/toggle", val);
      },
    },
    logo() {
      if (!this.settings.logo) {
        return;
      }

      if (typeof this.settings.logo === "object") {
        return this.settings.logo;
      }

      return {
        light: this.settings.logo,
        dark: this.settings.logo,
      };
    },
  },
  beforeMount() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      this.scrolled = window.scrollY;
    },
    scrollToTop() {
      if (window.innerWidth >= 1280) {
        return;
      }
      window.scrollTo(0, 0);
    },
    noop() {},
  },
});
</script>
