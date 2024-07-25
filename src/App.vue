<script setup>
import { ref, watch } from 'vue';
import { RouterLink, RouterView } from 'vue-router';

const isMenuOpen = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const closeMenu = () => {
  isMenuOpen.value = false;
};

watch(isMenuOpen, (newValue) => {
  if (newValue) {
    document.body.classList.add('no-scroll');
  } else {
    document.body.classList.remove('no-scroll');
  }
});
</script>

<template>
  <header>
    <RouterLink @click="closeMenu" to="/" class="logo">TOM | LEACH</RouterLink>
    <button @click="toggleMenu" class="menu-button">
      <svg v-if="!isMenuOpen" width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path class="line1" d="M4.96857 7.46857H24.9686" stroke="white" stroke-width="2.0" stroke-linecap="round" stroke-linejoin="round"/>
        <path class="line2" d="M4.96857 14.9686H24.9686" stroke="white" stroke-width="2.0" stroke-linecap="round" stroke-linejoin="round"/>
        <path class="line3" d="M4.96857 22.4686H24.9686" stroke="white" stroke-width="2.0" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
      <svg v-if="isMenuOpen" width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path class="line1" d="M6.25 6.25L23.75 23.75" stroke="white" stroke-width="2.0" stroke-linecap="round"/>
        <path class="line2" d="M6.25 23.75L23.75 6.25" stroke="white" stroke-width="2.0" stroke-linecap="round"/>
      </svg>
    </button>
  </header>
  <div :class="{ 'menu-open': isMenuOpen }" class="mobile-menu">
    <nav>
      <RouterLink to="/about" @click="closeMenu">About</RouterLink>
      <RouterLink to="/media" @click="closeMenu">Media</RouterLink>
      <RouterLink to="/contact" @click="closeMenu">Contact</RouterLink>
      <RouterLink to="/press" @click="closeMenu">Press</RouterLink>
    </nav>
  </div>
  <RouterView />
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  position: relative;
  z-index: 1000;
  position: fixed;
  width: 100vw;
  background: transparent;
}

.logo {
  font-weight:bold;
  font-size: 1.5rem;
  text-decoration: none;
  color: var(--color-text);
  line-height: 1;
  font-family: 'Urbanist-Regular';
}

.menu-button {
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  height: 30px;
  width: 30px;
}

.menu-button svg {
  height: 100%;
  width: 100%;
}

.mobile-menu {
  position: fixed;
  left: 0;
  top: 63px;
  width: 100%;
  height: calc(100dvh - 63px);
  background: var(--color-background);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.5s ease;
  z-index: 999;
}

.menu-open {
  opacity: 1;
  pointer-events: auto;
}

.menu-header {
  position: absolute;
  top: 1rem;
  left: 1rem;
  right: 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.mobile-menu nav {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  text-align: center;
}

.mobile-menu nav a {
  font-size: 2rem;
  color: var(--color-text);
  text-decoration: none;
  text-transform: lowercase;
  font-family: 'Urbanist-Regular';
}

@media screen and (min-width: 768px) {

  header {
    padding: 1rem 2rem;
  }

  .mobile-menu nav a {
    font-size: 3.0rem;
  }

  .logo {
    font-size: 2rem;
  }

  .menu-button {
  height: 35px;
  width: 35px;
}

}

</style>
