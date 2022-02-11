<template>
  <div class="pt-16 bg-gray-100">
    <AppHeader />

    <main class="container mx-auto px-4 lg:px-8" v-if="isDocNav">
      <div class="flex flex-wrap relative">
        <AppNav />
        <Nuxt class="w-full lg:w-4/5" />
      </div>
    </main>

    <Nuxt v-else />
  </div>
</template>

<script>
import _ from "lodash";
import { mapGetters } from "vuex";
import { useNav } from "~/plugins/nav";
import { defineComponent } from "@nuxtjs/composition-api";

export default defineComponent({
  head() {
    const i18nSeo = this.$nuxtI18nSeo();
    const previewUrl = this.settings.url.replace(/\/$/, "") + "/preview.png";

    return {
      titleTemplate: (chunk) => {
        if (chunk) {
          return `${chunk} - ${this.settings.title}`;
        }

        return this.settings.title;
      },
      bodyAttrs: {
        class: [
          ...this.bodyClass,
          "antialiased text-gray-700 leading-normal bg-white dark:bg-gray-900 dark:text-gray-300",
        ],
      },
      ...i18nSeo,
      meta: (i18nSeo.meta || []).concat([
        // Open Graph
        {
          hid: "og:site_name",
          property: "og:site_name",
          content: this.settings.title,
        },
        { hid: "og:type", property: "og:type", content: "website" },
        { hid: "og:url", property: "og:url", content: this.settings.url },
        { hid: "og:image", property: "og:image", content: previewUrl },
        // Twitter Card
        {
          hid: "twitter:card",
          name: "twitter:card",
          content: "summary_large_image",
        },
        {
          hid: "twitter:site",
          name: "twitter:site",
          content: this.settings.twitter,
        },
        {
          hid: "twitter:title",
          name: "twitter:title",
          content: this.settings.title,
        },
        { hid: "twitter:image", name: "twitter:image", content: previewUrl },
        {
          hid: "twitter:image:alt",
          name: "twitter:image:alt",
          content: this.settings.title,
        },
      ]),
    };
  },
  setup() {
    const { isHome, currentSlug } = useNav();
    return {
      isHome,
      currentSlug,
    };
  },

  computed: {
    ...mapGetters(["settings"]),
    bodyClass() {
      return this.$store.state.menu.open
        ? ["h-screen lg:h-auto overflow-y-hidden lg:overflow-y-auto"]
        : [];
    },
    isDocNav() {
      const currentSlug = this.currentSlug;
      const currentNav = _.find(this.settings.nav, (link) => {
        if (link.items) {
          let currentLink;
          _.each(link.items, (item) => {
            if (item.slug === currentSlug && link.name === "docs") {
              currentLink = item;
            }
          });
          return currentLink;
        }
      });
      return !_.isEmpty(currentNav);
    },
  },
});
</script>
