<script context="module">
  import { page } from '$app/stores'
  import About from '$components/about.svelte'
  import Head from '$components/head.svelte'
  import { client } from '$lib/graphql-client'
  import { authorsQuery } from '$lib/graphql-queries'
  import {
  fetchSiteMetadata,
  siteMetadataStore
  } from '$stores/site-metadata'
  import { marked } from 'marked'

  export const load = async () => {
    await fetchSiteMetadata()

    const { authors } = await client.request(authorsQuery)

    return {
      props: {
        authors,
      },
    }
  }
</script>

<script>
  export let authors

  const {
    name,
    intro,
    bio,
    picture: { url },
  } = authors[0]

  const {
    siteUrl,
    name: siteName,
    openGraphDefaultImage,
  } = $siteMetadataStore || []
</script>

<Head
  title={`Sobre mim · ${siteName}`}
  description={bio.slice(0, 120)}
  image={openGraphDefaultImage.url}
  url={`${siteUrl}${$page.url.pathname}`}
/>

<h1 class="font-bold text-center mb-20 text-5xl">Sobre mim</h1>

<About name={ name } intro={ intro } url={ url } />

<article div class="prose prose-lg">
  {@html marked(bio)}
</article>
