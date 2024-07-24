<script setup>
import { ref, watch } from 'vue';
import { RouterLink, RouterView } from 'vue-router';
import HamburgerMenuIcon from '@/assets/icons/HamburgerMenuIcon.vue';
import MenuCloseIcon from '@/assets/icons/MenuCloseIcon.vue';

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
    <RouterLink @click="closeMenu" to="/" class="logo">TOM/LEACH</RouterLink>
    <button @click="toggleMenu" class="menu-button">
      <component :is="isMenuOpen ? MenuCloseIcon : HamburgerMenuIcon" class="icon" :class="{ 'menu-open': isMenuOpen }"/>
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
}

.logo {
  font-weight: bold;
  font-size: 2.5rem;
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
  height: 35px;
  width: 35px;
}

.menu-button svg {
  height: 100%;
  width: 100%;
}

.mobile-menu {
  position: fixed;
  left: 0;
  width: 100%;
  height: calc(100dvh - 63px);
  background: var(--color-background);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
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
  gap: 2rem;
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

}

</style>
