<script context="module">
  import {
    authorsStore,
    fetchAuthors,
    fetchSocials,
    socialsStore,
  } from '$stores/site-metadata'
  import FacebookIcon from './facebook-icon.svelte'
  import TwitterIcon from './twitter-icon.svelte'
  import YouTubeIcon from './you-tube-icon.svelte'

  fetchAuthors()
  fetchSocials()
</script>

<script>
  const { twitterUrl, youTubeUrl, facebookUrl } = $socialsStore
  const { name: AuthorName } = $authorsStore
</script>

<footer
  class="p-10 footer bg-neutral text-neutral-content footer-center"
>
  <div class="grid grid-flow-col gap-4">
    <a class="link link-hover" href="/projetos">Portfólio</a>
    <!-- <a class="link link-hover" href="/posts">Posts</a> -->
    <a class="link link-hover" href="/sobre">Sobre mim</a>
  </div>
  <div>
    <div class="grid grid-flow-col gap-4">
      <a href={twitterUrl} target='_blank' rel='noopened nofollow'>
        <TwitterIcon />
      </a>
      <a href={youTubeUrl} target='_blank' rel='noopened nofollow'>
        <YouTubeIcon />
      </a>
      <a href={facebookUrl} target='_blank' rel='noopened nofollow'>
        <FacebookIcon />
      </a>
    </div>
  </div>
  <!-- <div>
    <p>
      Copyright &copy; {`${new Date().getFullYear()}`} - All right reserved
      {AuthorName}
    </p>
  </div> -->
</footer>
