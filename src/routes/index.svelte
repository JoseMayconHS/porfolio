<script context="module">
  import About from '$components/about.svelte'
  import Head from '$components/head.svelte'
  import ProjectCard from '$components/project-card.svelte'
  import { client } from '$lib/graphql-client'
  import { authorsQuery,projectsQuery } from '$lib/graphql-queries'
  import {
  authorsStore,
  fetchAuthors,
  fetchSiteMetadata,
  siteMetadataStore
  } from '$stores/site-metadata'

  export const load = async () => {
    await fetchAuthors()
    await fetchSiteMetadata()

    const [authorRes, projectsRes] = await Promise.all([
      client.request(authorsQuery),
      client.request(projectsQuery),
    ])
    const { authors } = authorRes
    const { projects } = projectsRes

    return {
      props: {
        projects: projects.reverse(),
        authors,
      },
    }
  }
</script>

<script>
  export let projects
  export let authors

  const {
    siteUrl,
    name: siteName,
    description,
    openGraphDefaultImage,
  } = $siteMetadataStore || []
  const { name: authorName } = $authorsStore || []
</script>

<Head
  title={`${siteName} · ${authorName}`}
  {description}
  image={openGraphDefaultImage.url}
  url={`${siteUrl}`}
/>

<h1 class="font-bold text-center mb-20 text-5xl">
  Bem-vindo ao meu portfólio
</h1>

{#each authors as { name, intro, picture: { url } }}
  <About name={ name } intro={ intro } url={ url } />
{/each}

<div
  class="grid gap-10 md:grid-cols-4 md:px-10 lg:grid-cols-6 lg:-mx-52"
>
  {#each projects as { name, slug, description, image }}
    <ProjectCard {name} {description} url={image[0].url} {slug} />
  {/each}
</div>
