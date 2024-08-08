<template>
  <div class="media container">
    <h1>MEDIA</h1>
    <p>Below is a playlist of songs I have worked on.</p>
    <p>Please contact me if you are looking for a more in depth catalogue of my work.</p>
    <div class="spotify_embed">
      <iframe style="border-radius:12px" src="https://open.spotify.com/embed/playlist/7fonVzgZw9enlvRlztIduw?utm_source=generator" width="100%" height="352" frameBorder="0"  allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>
    </div>
  </div>
</template>

<style>
  .media {
    display: flex;
    justify-content: center;
    padding: 75px 1rem 50px;
    height: max-content;
    width: 100%;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .spotify_embed {
    margin-top: 30px;
    width: 100%;
  }
  .spotify_embed iframe {
    height: 500px;
    max-width: 700px;
  }

  @media screen and (min-width: 768px) {
    .spotify_embed iframe {
    height: 700px;
  }
  }
</style>
