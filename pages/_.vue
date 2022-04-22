<template>
  <div
    class="flex flex-wrap-reverse"
    :class="{
      'lg:-mx-8': settings.layout === 'single'
    }"
    @click="handleClick"
  >
    <div
      class="w-full py-4 lg:pt-8 lg:pb-4 dark:border-gray-800"
      :class="{
        'lg:w-3/4': !document.fullscreen,
        'lg:border-l lg:border-r': settings.layout !== 'single'
      }"
    >
      <article class="prose dark:prose-dark max-w-none lg:px-8">
        <h1 class="flex items-center justify-between" v-if="document.badge">
          <Badge v-if="document.badge">{{ document.badge }}</Badge>
        </h1>
        <div v-if="document.subtitle" class="-mt-4">
          <p class="text-gray-600 dark:text-gray-400">{{ document.subtitle }}</p>
        </div>

        <NuxtContent :document="document" />
      </article>

      <AppPageBottom :document="document" :filePath="path" />
      <AppPrevNext :prev="prev" :next="next" />
    </div>

    <AppToc v-if="!document.fullscreen" :toc="document.toc" />
  </div>
</template>

<script>
import Vue from 'vue'
import { mapGetters } from 'vuex'
import _ from "lodash";

import AppCopyButton from '~/components/app/AppCopyButton'

export default {
  name: 'PageSlug',
  layout ({ store }) {
    return store.state.settings.layout || 'default'
  },
  middleware ({ app, params, redirect, store }) {
    if (params.pathMatch === 'index') {
      redirect(app.localePath('/'))
    }

    const path = params.pathMatch.split('/')
    const docsSetting = _.find(store.state.settings.nav, item => item.name ==='docs');
    const slugList = _.map(docsSetting.items, item => item.slug);
    if(_.includes(slugList, path[0]) && !path[1] ){
      redirect(app.localePath('/' + path[0] + '/readme'));
    }
  },
  async asyncData ({ $content, store, app, params, error }) {
    const path = `/${app.i18n.locale}/${params.pathMatch || 'index'}`
    const [document] = await $content({ deep: true }).where({ path }).fetch()
    if (!document) {
      return error({ statusCode: 404, message: 'Page not found' })
    }

    const [prev, next] = await $content(app.i18n.locale, { deep: true })
      .only(['title', 'path', 'to'])
      .sortBy('position', 'asc')
      .surround(document.path, { before: 1, after: 1 })
      .fetch()

    return {
      document,
      prev,
      next,
      path,
    }
  },
  head () {
    return {
      title: this.document.title,
      meta: [
        { hid: 'description', name: 'description', content: this.document.description },
        // Open Graph
        { hid: 'og:title', property: 'og:title', content: this.document.title },
        { hid: 'og:description', property: 'og:description', content: this.document.description },
        // Twitter Card
        { hid: 'twitter:title', name: 'twitter:title', content: this.document.title },
        { hid: 'twitter:description', name: 'twitter:description', content: this.document.description }
      ]
    }
  },
  methods: {
    handleClick(event) {
      const aTag = _.find(event.path || (event?.composedPath()) , item => (item.nodeName?.toLowerCase() === 'a'))
      if(!aTag) return;

      if (event.preventDefault) {
        event.preventDefault();
      } else {
        window.event.returnValue = true;
      }

      let url = aTag.getAttribute("href");
      url = decodeURI(url);
      if(_.startsWith(url, '#')){
        url = url.toLowerCase();
      }

      const docs = _.find(this.settings.nav, {'name': 'docs' }).items;

      if (aTag.getAttribute("target") === '_blank') {
        window.open(url)
      } else {
        url = url.replace(/.md|zh\//ig, '' );
        _.forEach(docs, (item) => {
          if(!item.redirect) return;
          _.forEach(item.redirect, (val,key) =>{
            if(_.includes(url, key)){
              url = url.replace(key, val);
              return;
            }
          })
        })
        this.$router.push(url);
      }
    }
  },
  computed: {
    ...mapGetters([
      'settings'
    ])
  },
  mounted () {
    if (this.document.version) {
      localStorage.setItem(`document-${this.document.slug}-version`, this.document.version)
    }

    setTimeout(() => {
      const blocks = document.getElementsByClassName('nuxt-content-highlight')

      for (const block of blocks) {
        const CopyButton = Vue.extend(AppCopyButton)
        const component = new CopyButton().$mount()
        block.appendChild(component.$el)
      }
    }, 100)
  }
}
</script>
