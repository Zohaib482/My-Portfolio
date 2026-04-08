<script setup lang="ts">
import { onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  // Navbar entrance animation
  const navTl = gsap.timeline()
  navTl.from('.navbar', {
    y: -100,
    opacity: 0,
    duration: 1,
    ease: 'power4.out'
  }).from('.nav-link', {
    y: -20,
    opacity: 0,
    stagger: 0.1,
    duration: 0.8,
    ease: 'power3.out'
  }, '-=0.5')

  // Smart navbar: hide on scroll down, show on scroll up
  let lastScroll = 0
  ScrollTrigger.create({
    start: 'top top',
    end: 99999,
    onUpdate: (self) => {
      const currentScroll = self.scroll()
      const navbar = document.querySelector('.navbar')
      if (navbar) {
        if (currentScroll > lastScroll && currentScroll > 100) {
          // Scrolling down
          gsap.to(navbar, { y: '-100%', duration: 0.3, ease: 'power2.inOut' })
        } else {
          // Scrolling up
          gsap.to(navbar, { y: '0%', duration: 0.3, ease: 'power2.inOut' })
        }
      }
      lastScroll = currentScroll
    }
  })

  // Setup mobile menu toggle
  const toggleMobileMenu = () => {
    const navMenu = document.querySelector('.nav-menu')
    const isActive = navMenu?.classList.toggle('active')
    
    if (isActive) {
      gsap.from('.nav-menu .nav-link', {
        x: -50,
        opacity: 0,
        stagger: 0.1,
        duration: 0.5,
        ease: 'power2.out'
      })
    }
  }

  // Make toggleMobileMenu available globally for template
  ;(window as any).toggleMobileMenu = toggleMobileMenu
})
</script>

<template>
  <div id="app">
    <nav class="navbar">
      <div class="container">
        <div class="nav-brand">Zohaib Khan</div>
        <ul class="nav-menu">
          <li><a href="#home" class="nav-link">Home</a></li>
          <li><a href="#about" class="nav-link">About</a></li>
          <li><a href="#skills" class="nav-link">Skills</a></li>
          <li><a href="#experience" class="nav-link">Experience</a></li>
          <li><a href="#projects" class="nav-link">Projects</a></li>
          <li><a href="#contact" class="nav-link">Contact</a></li>
        </ul>
        <div class="nav-toggle" onclick="toggleMobileMenu()">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
    </nav>

    <router-view />
  </div>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  background-color: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--border-color);
  z-index: 1000;
  padding: 1rem 0;
}

.navbar .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand {
  font-family: 'Playfair Display', serif;
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--primary-color);
}

.nav-menu {
  display: flex;
  list-style: none;
  gap: 2rem;
}

.nav-link {
  color: var(--text-primary);
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s ease;
}

.nav-link:hover {
  color: var(--primary-color);
}

.nav-toggle {
  display: none;
  flex-direction: column;
  cursor: pointer;
}

.nav-toggle span {
  width: 25px;
  height: 3px;
  background-color: var(--text-primary);
  margin: 3px 0;
  transition: 0.3s;
}

@media (max-width: 768px) {
  .nav-menu {
    position: fixed;
    left: -100%;
    top: 70px;
    flex-direction: column;
    background-color: white;
    width: 100%;
    text-align: center;
    transition: 0.3s;
    box-shadow: var(--shadow-lg);
    padding: 2rem 0;
  }

  .nav-menu.active {
    left: 0;
  }

  .nav-toggle {
    display: flex;
  }
}
</style>
