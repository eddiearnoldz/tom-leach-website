<template>
  <div class="about container">
    <h1>About me</h1>
    <p>Tom “TL” Leach is a writer, producer, mixer and recording engineer based in East London. Over the past decade, he's had the opportunity to work with a wide range of talented artists, including Fergie, Lewis Capaldi, Burna Boy, Headie One, Tribes, Pa Salieu, Tion Wayne, Antslive, Shy FX, Mr Scruff, FKA Twigs, Riz Ahmed, Years and Years, Stormzy, Wretch 32, Clean Bandit, Deaf Havana, Spiritualized, Beth Gibbons, James Ford, Jerry Boys, Haydn Bendall, and many others.</p>
    <p>Recent projects include mix/mastering across <a href="https://open.spotify.com/artist/3JYp3dC5wTBWagBRR5fjpk?si=41lU5Y8fSPutPvFx7Ol-MQ" target="_blank">AntsLive’s</a> breakout into mainstream hip-hop, and co-writing/producing/mixing all of <a href="https://open.spotify.com/artist/538iX6YCTybcgzsrjDTrFi?si=7Lv_yPfOSmO7yvlCnVP8jw" target="_blank"> LEAP’s  </a>ascent as one the fastest growing rock projects in Europe. </p>
    
    <img src="/assets/tom_leach_pic.webp" alt="Tom in the studio">

    <h2>PRESS HIGHLIGHTS</h2>

    <div class="highlights">
      <div class="highlight">
        <p class="quote">“UK Rap Anthem of the future”</p>
        <p class="publication">- NME (AntsLive) </p>
      </div>
      <div class="highlight">
        <p class="quote">“Vigorous, adventurous, powerful tracks, this band will be seen on big stages” </p>
        <p class="publication">- ROLLING STONE (LEAP) </p>
      </div>
      <div class="highlight">
        <p class="quote">"a rush of explosive pop-rock"</p>
        <p class="publication">- LINE OF BEST FIT (modernlove.)</p>
      </div>
      <div class="highlight">
        <p class="quote">“Experimental, dynamic, refreshing guitar sound”</p>
        <p class="publication">- MTV (LEAP) </p>
      </div>
    </div>


  </div>
</template>

<style scoped>
  .about {
    display: flex;
    justify-content: center;
    padding: 10rem 1rem 0;
    height: max-content;
    max-width: 1000px;
    width: 100%;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 0 auto;
    text-align: center;;
  }

  .about a {
    color: #1C9BEF;
    text-decoration: none;
  }

  .about img {
    max-width: 500px;
    margin: 50px;
    border-radius: 2px;
    width: 100%;
  }

  .about h2 {
    font-weight: 700;
    font-size: 1.5rem;
  }

  .highlights {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .highlight {
    display: flex;
    flex-direction: column;
  }

  .quote {
    font-style: italic;
    margin: 0;
  }

  .publication {
    font-weight: 700;
    margin: 0;
  }

  @media screen and (min-width: 768px) {
    .about {
      padding: 10rem 4rem 0;
    }

    .about h2 {
      font-size: 1.9rem;
    }
  }
</style>
