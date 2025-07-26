<script setup>
import { ref, watch } from 'vue';
import { RouterLink, RouterView } from 'vue-router';

const isMenuOpen = ref(false);
const isLoading = ref(false);
const clickedElement = ref(null);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const closeMenu = () => {
  isMenuOpen.value = false;
};

const handleClick = (event) => {
  isLoading.value = true;
  setTimeout(() => {
    isLoading.value = false;
    closeMenu();
  }, 1000); // 1 second delay
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
  <header :class="{ 'loading': isLoading }">
    <RouterLink @click="handleClick" to="/" class="logo">
      <span >TOM | LEACH</span>
      <span >writer | producer | mixer | engineer</span>
    </RouterLink>
    <button @click="toggleMenu" class="menu-button" aria-label="toggle menu button">
      <svg v-if="!isMenuOpen" width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path class="line1" d="M4.96857 7.46857H24.9686" stroke="white" stroke-width="2.0" stroke-linecap="round" stroke-linejoin="round"/>
        <path class="line2" d="M4.96857 14.9686H24.9686" stroke="white" stroke-width="2.0" stroke-linecap="round" stroke-linejoin="round"/>
        <path class="line3" d="M4.96857 22.4686H24.9686" stroke="white" stroke-width="2.0" stroke-linecap="round"/>
      </svg>
      <svg v-if="isMenuOpen" width="30" height="30" viewBox="0 0 30 30" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path class="line1" d="M6.25 6.25L23.75 23.75" stroke="white" stroke-width="2.0" stroke-linecap="round"/>
        <path class="line2" d="M6.25 23.75L23.75 6.25" stroke="white" stroke-width="2.0" stroke-linecap="round"/>
      </svg>
    </button>
  </header>
  <div :class="{ 'menu-open': isMenuOpen, 'loading': isLoading }" class="mobile-menu">
    <nav>
      <RouterLink to="/about" @click="handleClick" >About</RouterLink>
      <RouterLink to="/media" @click="handleClick" >Media</RouterLink>
      <RouterLink to="/contact" @click="handleClick">Contact</RouterLink>
    </nav>
  </div>
  <div :class="{ 'loading': isLoading }" class="content">
    <router-view />
  </div>
</template>

<style scoped>
/* Global Styles */
body.no-scroll {
  overflow: hidden;
}

/* Header and Menu Styles */
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  position: relative;
  z-index: 1000;
  position: fixed;
  width: 100vw;
  background: linear-gradient(to bottom, rgba(0, 0, 0, 1), rgba(0, 0, 0, 0));
}

.logo {
  text-decoration: none;
  display: flex;
  flex-direction: column;
  gap: 3px;
}

.logo span {
  font-weight: bold;
  font-size: 1.925rem;
  color: var(--color-text);
  line-height: 1;
  font-family: 'Urbanist-Regular';
  transition: color 0.3s;
}

.logo span:last-of-type {
  font-size: .75rem;
  padding-left: 2px;
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
  top: 0;
  width: 100%;
  height: 100vh;
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

/* Blur and Loading Styles */


.loading.mobile-menu nav a.router-link-active {
  color: #ff3e28;
  animation: scaleInOutMobile 0.8s ease-in-out forwards;
}


@media screen and (min-width: 768px) {
  header {
    padding: 1rem 2rem;
  }

  .mobile-menu nav a {
    font-size: 3.0rem;
    transition: color 0.3s, transform 0.3s;
  }

  .mobile-menu nav a:hover {
    font-size: 3.0rem;
    color: #ff3e28;
    transition: color 0.3s, transform 0.3s forwards;
    transform: scale(1.1);
  }

  .logo:hover span {
    color: #ff3e28;
    transition: color 0.3s;
  }

  .logo span {
    font-size: 2.55rem;
  }

  .logo span:last-of-type {
    font-size: 1rem;
  }

  .menu-button {
    height: 35px;
    width: 35px;
    transition: color 0.3s, transform 0.3s;
  }

  .menu-button {
    height: 35px;
    width: 35px;
  }

  .menu-button svg path {
    transition: stroke 0.3s;
  }

  .menu-button:hover svg path {
    stroke: #ff3e28;
    transition: stroke 0.3s;
  }

  .loading.mobile-menu nav a.router-link-active {
    stroke: #ff3e28;
    animation: scaleInOutDesktop 0.8s ease-in-out forwards;
  }
}

@keyframes scaleInOutMobile {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
}

@keyframes scaleInOutDesktop {
  0%, 100% {
    transform: scale(1.1);
  }
  50% {
    transform: scale(1);
  }
}
</style>
