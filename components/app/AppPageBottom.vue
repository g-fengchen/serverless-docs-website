<template>
  <div v-if="link" class="pt-4 pb-4 lg:px-8 flex flex-col sm:flex-row justify-between">
    <a
      :href="link"
      target="_blank"
      rel="noopener"
      class="text-gray-600 dark:text-gray-400 text-sm font-medium hover:underline flex items-center"
    >
      {{ $t('article.github') }}
      <IconExternalLink class="w-4 h-4 ml-1" />
    </a>
    <span class="text-gray-600 dark:text-gray-400 text-sm font-medium flex items-center">
      {{ $t("article.updatedAt") }} {{ $d(Date.parse(document.updatedAt), "long") }}
    </span>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import _ from "lodash"

export default {
  props: {
    document: {
      type: Object,
      required: true
    },
    filePath: {
      type: String,
      required: true
    }
  },
  computed: {
    ...mapGetters([
      'settings',
      'githubUrls'
    ]),
    link () {
      if (!this.settings.github) {
        return
      }
      const docUrls = _.split(this.filePath, '/').filter(path => !!path)
      const [lang, repo, ...file] = docUrls

      const repoUrl = repo === 'fc' ? this.githubUrls.fcRepo : this.githubUrls.repo
      const defaultBranch = repo === 'fc' ? 'main' : 'master'
      const filePath = file.join('/')

      return [
        repoUrl,
        'edit',
        defaultBranch,
        this.settings.defaultDir,
        `${lang}/${filePath}${this.document.extension}`
      ].filter(path => !!path).join('/')
    }
  }
}
</script>
