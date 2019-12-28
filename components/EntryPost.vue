<template lang="pug">
ContentContainer
  div.entry-lead(slot="lead")
    h1.entry-title {{ entry.title }}
    h3(v-if="entry.description").entry-description {{ entry.description }}

  section.entry-body(slot="content" :style="overrideMargin")
    div(v-html="entry.body")
    // ShareWidgets(:entry="entry")

  div.entry-closer(slot="closer")
    img.entry-image(v-if="entry.image" :src="`/img/entrys/${entry.image}`")
    p(v-if="entry.quote" v-html="entry.quote").entry-quote
</template>

<script>
import ContentContainer from '~/components/ContentContainer'

export default {
  props: {
    entry: { type: Object }
  },

  head () {
    return {
      title: 'Alid Castano | ' + this.entry.title,
      meta: [
        { name: 'description', hid: 'description', content: this.entry.description },
        // Open Graph
        { name: 'og:title', content: this.entry.title },
        { name: 'og:description', content: this.entry.description },
        { name: 'og:type', content: 'website' },
        { name: 'og:url', content: `https://alidcastano.com/${this.entry.permalink}` },
        { name: 'og:image', content: `https://alidcastano.com/img/entrys/${this.entry.image}` },
        // Twitter Card
        { name: 'twitter:card', content: 'summary' },
        { name: 'twitter:site', content: '@alidcastano' },
        { name: 'twitter:title', content: this.entry.title },
        { name: 'twitter:description', content: this.entry.description },
        { name: 'twitter:image', content: `https://alidcastano.com/img/entrys/${this.entry.image}` },
        { name: 'twitter:image:alt', content: this.entry.title }
      ]
    }
  },

  computed: {
    overrideMargin () {
      if (this.entry.title.length > 30) return { 'margin-left': '1rem' }
    }
  },

  components: {
    ContentContainer
    // ShareWidgets: () => import('~/components/ShareWidgets')
  }
}
</script>

<style lang="sass" scope>
@import "../assets/sass/util"

.entry-lead
  margin-top: 16px
  margin-bottom: 1.25rem
  width: 100%
  @media (min-width: $bp-tablet)
    margin-bottom: 1.75rem
  .entry-title
    font-size: 1.6rem
    color: #45606e
    margin: 0
    @media (min-width: $bp-tablet)
      font-size: 2.125rem
  .entry-description
    font-size: 1rem
    margin-top: 4px
    color: #9fa5ad
    font-weight: normal
    font-style: italic
    @media (min-width: $bp-tablet)
      font-size: 1.125rem
.entry-body
  font-family: Spectral,serif;
  hr 
    width: 90%
    margin-left: auto
    margin-right: auto
  a 
    text-decoration: underline
br 
  display: block
  content: " "
  margin-top: 4px
  
.entry-closer
  margin-top: 3rem
  margin-bottom: 4rem
.entry-image
  margin: .5rem auto 1rem auto
.entry-quote
  margin: 0 auto
  color: #838b95
  font-style: italic
  font-size: .9rem
  @media (min-width: $bp-tablet)
    max-width: 85%
  a 
    color: #838b95
    text-decoration: underline
  span 
    display: block 
    margin-top: .25rem
    @media (min-width: $bp-tablet)
      text-align: right
      position: relative 
      right: 2rem
</style>