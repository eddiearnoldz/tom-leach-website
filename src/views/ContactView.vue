<script>
import SvgIcon from '../components/SvgIcon.vue';
export default {
  components: {
    SvgIcon
  }
}
</script>

<template>
  <div class="contact container">
    <h1>Contact</h1>
    <p>
      Looking to record your next project?
    </p>
    <p>
      I'm happy working anywhere, whether it's your home studio, the studios I work in, or on location. I'm equally at home on a large console as I am working "in the box".
    </p>
    <p>
      Get in touch to see what I can do for you.
    </p>
    <p>
      Rates available on request.
    </p>

    <div class="contact_icons">
      <a class="contact_icon facebook" href="http://facebook.com/tslleach" target="_blank" alt="facebook-icon"><SvgIcon name="facebook-icon" /></a>
      <a class="contact_icon twitter" href="http://twitter.com/tslleach" target="_blank" alt="twitter-icon"><SvgIcon name="twitter-icon" /></a>
      <a class="contact_icon mail" href="mailto:tom@snapstudios.co.uk" target="_blank" alt="Mail" aria-label="Mail"><SvgIcon name="mail-icon" /></a>
    </div>
  </div>
</template>

<style>
 .contact {
  text-align: center;
 }

 .contact_icons {
  display: flex;
  gap: 10px;
  place-items: center;
  justify-content: center;
  align-items: center;
 }

 .contact_icon {
  height: 30px;
  width: 30px;
  transition-duration: 0.3s;
 }

a.contact_icon path {
  fill: #333333;
  transition-duration: 0.3s;
}

a.contact_icon.facebook:hover path {
  fill: #1977F2;
}

a.contact_icon.mail:hover path {
  fill: #EA4335;
  transition-duration: 0.3s;
}

a.contact_icon.twitter:hover path {
  fill: #1C9BEF;
  transition-duration: 0.3s;
}


</style>
