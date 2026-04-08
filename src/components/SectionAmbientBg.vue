<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const root = ref<HTMLElement | null>(null)

onMounted(() => {
  const el = root.value
  if (!el) return
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return

  const shapes = el.querySelectorAll<HTMLElement>('.ambient-shape')
  shapes.forEach((shape, i) => {
    const dir = i % 2 === 0 ? 1 : -1
    gsap.to(shape, {
      y: 30 * dir,
      rotation: 12 * dir,
      duration: 10 + i * 2.5,
      repeat: -1,
      yoyo: true,
      ease: 'sine.inOut',
      delay: i * 0.4
    })
  })

  const orbs = el.querySelectorAll<HTMLElement>('.ambient-orb')
  orbs.forEach((orb, i) => {
    gsap.to(orb, {
      scale: 1.15,
      opacity: 0.55,
      duration: 5 + i * 1.2,
      repeat: -1,
      yoyo: true,
      ease: 'sine.inOut',
      delay: i * 0.35
    })
  })
})
</script>

<template>
  <div ref="root" class="section-ambient" aria-hidden="true">
    <!-- Slow-moving dot field (always reads on white / off-white) -->
    <div class="ambient-dots"></div>

    <!-- Soft color washes -->
    <div class="ambient-orb ambient-orb--1"></div>
    <div class="ambient-orb ambient-orb--2"></div>

    <!-- Elegant floating frame shapes (outline, hero-adjacent language) -->
    <div class="ambient-shape ambient-shape--1"></div>
    <div class="ambient-shape ambient-shape--2"></div>
    <div class="ambient-shape ambient-shape--3"></div>
    <div class="ambient-shape ambient-shape--4"></div>

    <!-- Sheen that crawls across the section -->
    <div class="ambient-sheen"></div>
  </div>
</template>

<style scoped>
.section-ambient {
  position: absolute;
  inset: 0;
  z-index: 0;
  pointer-events: none;
  overflow: hidden;
}

/* Visible dot lattice — subtle but unmistakable motion */
.ambient-dots {
  position: absolute;
  inset: -20%;
  background-image: radial-gradient(circle at center, rgba(99, 102, 241, 0.14) 1.2px, transparent 1.5px);
  background-size: 28px 28px;
  animation: ambient-dots-drift 24s linear infinite;
  opacity: 0.65;
  mask-image: radial-gradient(ellipse 75% 70% at 50% 48%, black 12%, transparent 72%);
}

@keyframes ambient-dots-drift {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 28px 28px;
  }
}

.ambient-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(40px);
  pointer-events: none;
  will-change: transform, opacity;
}

.ambient-orb--1 {
  width: min(70vw, 520px);
  height: min(55vw, 420px);
  left: -18%;
  top: -8%;
  background: radial-gradient(circle, rgba(99, 102, 241, 0.22) 0%, rgba(129, 140, 248, 0.08) 55%, transparent 72%);
  opacity: 0.75;
}

.ambient-orb--2 {
  width: min(65vw, 480px);
  height: min(60vw, 440px);
  right: -20%;
  bottom: -15%;
  background: radial-gradient(circle, rgba(118, 75, 162, 0.2) 0%, rgba(99, 102, 241, 0.07) 50%, transparent 70%);
  opacity: 0.7;
}

.ambient-shape {
  position: absolute;
  border: 1.5px solid rgba(99, 102, 241, 0.28);
  border-radius: 28%;
  background: linear-gradient(
    135deg,
    rgba(99, 102, 241, 0.06) 0%,
    rgba(255, 255, 255, 0.02) 100%
  );
  will-change: transform;
}

.ambient-shape--1 {
  width: 88px;
  height: 88px;
  left: 6%;
  top: 18%;
  rotate: -18deg;
}

.ambient-shape--2 {
  width: 64px;
  height: 64px;
  right: 10%;
  top: 28%;
  border-radius: 50%;
  rotate: 12deg;
}

.ambient-shape--3 {
  width: 120px;
  height: 72px;
  right: 6%;
  bottom: 22%;
  border-radius: 999px;
  rotate: -8deg;
}

.ambient-shape--4 {
  width: 56px;
  height: 56px;
  left: 12%;
  bottom: 25%;
  border-radius: 12px;
  rotate: 25deg;
}

.ambient-sheen {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    105deg,
    transparent 0%,
    transparent 40%,
    rgba(255, 255, 255, 0.22) 48%,
    rgba(129, 140, 248, 0.12) 52%,
    transparent 60%,
    transparent 100%
  );
  background-size: 200% 100%;
  animation: ambient-sheen-move 14s ease-in-out infinite;
  opacity: 0.45;
  mix-blend-mode: soft-light;
}

@keyframes ambient-sheen-move {
  0%,
  100% {
    background-position: 130% 0;
  }
  50% {
    background-position: -30% 0;
  }
}

@media (prefers-reduced-motion: reduce) {
  .ambient-dots,
  .ambient-sheen {
    animation: none;
  }

  .ambient-dots {
    opacity: 0.4;
  }

  .ambient-sheen {
    opacity: 0.15;
    background-position: 50% 0;
  }
}
</style>
