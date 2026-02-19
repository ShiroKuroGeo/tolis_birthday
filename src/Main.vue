<script setup>
import { ref, computed, onMounted } from 'vue';

const svg3 = `
<svg viewBox="0 0 220 240" width="220" height="240" fill="none" xmlns="http://www.w3.org/2000/svg">
  <rect class="confetti-bit" x="18" y="20" width="8" height="8" rx="2" fill="#FFD93D" style="animation-delay:.1s"/>
  <rect class="confetti-bit" x="170" y="10" width="7" height="7" rx="1" fill="#FF6B9D" style="animation-delay:.4s"/>
  <rect class="confetti-bit" x="55" y="8" width="6" height="10" rx="2" fill="#C56CF0" style="animation-delay:.7s"/>
  <rect class="confetti-bit" x="150" y="30" width="8" height="5" rx="1" fill="#4FC3F7" style="animation-delay:.2s"/>
  <rect class="confetti-bit" x="195" y="50" width="6" height="6" rx="1" fill="#FFD93D" style="animation-delay:.9s"/>
  <rect class="confetti-bit" x="10" y="60" width="5" height="9" rx="2" fill="#FF6B9D" style="animation-delay:.5s"/>
  <polygon class="twinkle" points="30,42 32,36 34,42 40,42 35,46 37,52 32,48 27,52 29,46 24,42" fill="#FFD93D" style="animation-delay:.3s; transform-origin:32px 44px"/>
  <polygon class="twinkle" points="188,25 190,19 192,25 198,25 193,29 195,35 190,31 185,35 187,29 182,25" fill="#FF6B9D" style="animation-delay:.8s; transform-origin:190px 27px"/>
  <rect x="30" y="178" width="160" height="44" rx="22" fill="#FF6B9D"/>
  <rect x="40" y="178" width="140" height="20" rx="10" fill="#FF8FB3"/>
  <ellipse cx="60" cy="178" rx="8" ry="6" fill="#fff" opacity=".7"/>
  <ellipse cx="100" cy="175" rx="10" ry="7" fill="#fff" opacity=".7"/>
  <ellipse cx="140" cy="178" rx="9" ry="6" fill="#fff" opacity=".7"/>
  <ellipse cx="175" cy="177" rx="7" ry="5" fill="#fff" opacity=".7"/>
  <rect x="50" y="130" width="120" height="50" rx="18" fill="#C56CF0"/>
  <rect x="60" y="130" width="100" height="22" rx="11" fill="#D987F5"/>
  <ellipse cx="80" cy="130" rx="8" ry="5" fill="#fff" opacity=".6"/>
  <ellipse cx="115" cy="127" rx="9" ry="6" fill="#fff" opacity=".6"/>
  <ellipse cx="150" cy="130" rx="7" ry="5" fill="#fff" opacity=".6"/>
  <rect x="72" y="90" width="76" height="42" rx="14" fill="#FFD93D"/>
  <rect x="80" y="90" width="60" height="18" rx="9" fill="#FFE770"/>
  <ellipse cx="95" cy="90" rx="6" ry="4" fill="#fff" opacity=".5"/>
  <ellipse cx="120" cy="87" rx="7" ry="5" fill="#fff" opacity=".5"/>
  <ellipse cx="145" cy="90" rx="5" ry="4" fill="#fff" opacity=".5"/>
  <rect x="88" y="68" width="8" height="24" rx="4" fill="#4FC3F7"/>
  <rect x="106" y="62" width="8" height="30" rx="4" fill="#FF6B9D"/>
  <rect x="124" y="68" width="8" height="24" rx="4" fill="#FFD93D"/>
  <ellipse cx="92" cy="65" rx="4" ry="6" fill="#FFD93D"/>
  <ellipse cx="92" cy="64" rx="2" ry="3" fill="#FF6B9D" opacity=".8"/>
  <ellipse cx="110" cy="59" rx="4" ry="6" fill="#FFD93D"/>
  <ellipse cx="110" cy="58" rx="2" ry="3" fill="#FF6B9D" opacity=".8"/>
  <ellipse cx="128" cy="65" rx="4" ry="6" fill="#FFD93D"/>
  <ellipse cx="128" cy="64" rx="2" ry="3" fill="#FF6B9D" opacity=".8"/>
  <rect x="16" y="198" width="36" height="24" rx="5" fill="#9B30D0"/>
  <rect x="16" y="198" width="36" height="10" rx="3" fill="#C56CF0"/>
  <rect x="32" y="195" width="4" height="30" rx="2" fill="#FFD93D"/>
  <rect x="16" y="205" width="36" height="4" rx="1" fill="#FFD93D"/>
  <rect x="168" y="200" width="30" height="22" rx="5" fill="#FF6B9D"/>
  <rect x="168" y="200" width="30" height="9" rx="3" fill="#FF8FB3"/>
  <rect x="181" y="197" width="4" height="28" rx="2" fill="#fff"/>
  <rect x="168" y="207" width="30" height="4" rx="1" fill="#fff"/>
</svg>`;

const svg2 = `
<svg viewBox="0 0 220 240" width="220" height="240" fill="none" xmlns="http://www.w3.org/2000/svg">
  <rect class="confetti-bit" x="14" y="15" width="7" height="7" rx="2" fill="#FFD93D" style="animation-delay:.2s"/>
  <rect class="confetti-bit" x="180" y="8" width="8" height="6" rx="1" fill="#4FC3F7" style="animation-delay:.6s"/>
  <rect class="confetti-bit" x="60" y="5" width="6" height="10" rx="2" fill="#FF6B9D" style="animation-delay:.4s"/>
  <rect class="confetti-bit" x="155" y="25" width="8" height="5" rx="1" fill="#FFD93D" style="animation-delay:.1s"/>
  <rect class="confetti-bit" x="195" y="55" width="6" height="6" rx="1" fill="#C56CF0" style="animation-delay:.8s"/>
  <polygon class="twinkle" points="22,90 24,84 26,90 32,90 27,94 29,100 24,96 19,100 21,94 16,90" fill="#FFD93D" style="animation-delay:.1s; transform-origin:24px 92px"/>
  <polygon class="twinkle" points="192,75 194,69 196,75 202,75 197,79 199,85 194,81 189,85 191,79 186,75" fill="#FF6B9D" style="animation-delay:.5s; transform-origin:194px 77px"/>
  <polygon class="twinkle" points="40,35 41.5,30 43,35 48,35 44,38 45.5,43 41.5,40 37.5,43 39,38 35,35" fill="#C56CF0" style="animation-delay:.9s; transform-origin:41px 36px"/>
  <rect x="24" y="182" width="172" height="46" rx="23" fill="#9B30D0"/>
  <rect x="34" y="182" width="152" height="22" rx="11" fill="#C56CF0"/>
  <ellipse cx="58" cy="182" rx="10" ry="7" fill="#fff" opacity=".6"/>
  <ellipse cx="110" cy="178" rx="12" ry="8" fill="#fff" opacity=".6"/>
  <ellipse cx="162" cy="182" rx="10" ry="7" fill="#fff" opacity=".6"/>
  <circle cx="70" cy="200" r="8" fill="#FF6B9D"/>
  <circle cx="70" cy="200" r="5" fill="#FF8FB3"/>
  <circle cx="70" cy="200" r="2" fill="#FFD93D"/>
  <circle cx="150" cy="200" r="8" fill="#FF6B9D"/>
  <circle cx="150" cy="200" r="5" fill="#FF8FB3"/>
  <circle cx="150" cy="200" r="2" fill="#FFD93D"/>
  <rect x="50" y="130" width="120" height="54" rx="20" fill="#FF6B9D"/>
  <rect x="60" y="130" width="100" height="25" rx="12" fill="#FF8FB3"/>
  <ellipse cx="82" cy="130" rx="9" ry="6" fill="#fff" opacity=".6"/>
  <ellipse cx="110" cy="126" rx="11" ry="7" fill="#fff" opacity=".6"/>
  <ellipse cx="140" cy="130" rx="9" ry="6" fill="#fff" opacity=".6"/>
  <circle cx="90" cy="152" r="7" fill="#C56CF0"/>
  <circle cx="90" cy="152" r="4" fill="#D987F5"/>
  <circle cx="90" cy="152" r="2" fill="#FFD93D"/>
  <circle cx="130" cy="152" r="7" fill="#C56CF0"/>
  <circle cx="130" cy="152" r="4" fill="#D987F5"/>
  <circle cx="130" cy="152" r="2" fill="#FFD93D"/>
  <g class="bounce-person">
    <rect x="98" y="68" width="24" height="36" rx="8" fill="#4FC3F7"/>
    <circle cx="110" cy="56" r="16" fill="#FBBF7C"/>
    <path d="M94 52 Q110 36 126 52" fill="#5B21B6"/>
    <circle cx="105" cy="56" r="2" fill="#333"/>
    <circle cx="115" cy="56" r="2" fill="#333"/>
    <path d="M105 62 Q110 67 115 62" stroke="#333" stroke-width="1.5" stroke-linecap="round" fill="none"/>
    <path d="M98 78 Q78 55 68 40" stroke="#FBBF7C" stroke-width="8" stroke-linecap="round"/>
    <circle cx="66" cy="38" r="6" fill="#FBBF7C"/>
    <path d="M122 78 Q142 55 152 40" stroke="#FBBF7C" stroke-width="8" stroke-linecap="round"/>
    <circle cx="154" cy="38" r="6" fill="#FBBF7C"/>
    <path d="M98 90 Q85 115 80 130 L140 130 Q135 115 122 90 Z" fill="#FF6B9D"/>
  </g>
  <polygon class="twinkle" points="56,30 58,24 60,30 66,30 61,34 63,40 58,36 53,40 55,34 50,30" fill="#FFD93D" style="animation-delay:.2s; transform-origin:58px 32px"/>
  <polygon class="twinkle" points="156,28 158,22 160,28 166,28 161,32 163,38 158,34 153,38 155,32 150,28" fill="#FFD93D" style="animation-delay:.7s; transform-origin:158px 30px"/>
</svg>`;

const svg1 = `
<svg viewBox="0 0 220 240" width="220" height="240" fill="none" xmlns="http://www.w3.org/2000/svg">
  <ellipse cx="30" cy="40" rx="16" ry="20" fill="#FFD93D"/>
  <line x1="30" y1="60" x2="35" y2="90" stroke="#FFD93D" stroke-width="1.5"/>
  <ellipse cx="55" cy="25" rx="14" ry="18" fill="#FF6B9D"/>
  <line x1="55" y1="43" x2="52" y2="90" stroke="#FF6B9D" stroke-width="1.5"/>
  <ellipse cx="185" cy="35" rx="15" ry="19" fill="#4FC3F7"/>
  <line x1="185" y1="54" x2="180" y2="90" stroke="#4FC3F7" stroke-width="1.5"/>
  <rect class="confetti-bit" x="75" y="10" width="7" height="7" rx="2" fill="#C56CF0" style="animation-delay:.3s"/>
  <rect class="confetti-bit" x="160" y="15" width="6" height="9" rx="2" fill="#FFD93D" style="animation-delay:.6s"/>
  <rect class="confetti-bit" x="200" y="60" width="7" height="5" rx="1" fill="#FF6B9D" style="animation-delay:.1s"/>
  <polygon class="twinkle" points="140,12 142,6 144,12 150,12 145,16 147,22 142,18 137,22 139,16 134,12" fill="#FFD93D" style="animation-delay:.4s; transform-origin:142px 14px"/>
  <image href="/tolits.png" x="60" y="70" width="100" height="100" />
  <rect x="10" y="155" width="22" height="34" rx="8" fill="#FFD93D"/>
  <circle cx="21" cy="145" r="14" fill="#FBBF7C"/>
  <path d="M7 142 Q21 130 35 142" fill="#5B21B6"/>
  <circle cx="17" cy="145" r="2" fill="#333"/>
  <circle cx="25" cy="145" r="2" fill="#333"/>
  <path d="M17 150 Q21 154 25 150" stroke="#333" stroke-width="1.5" fill="none" stroke-linecap="round"/>
  <path d="M10 163 Q-2 148 -4 138" stroke="#FBBF7C" stroke-width="7" stroke-linecap="round"/>
  <path d="M32 163 Q46 158 58 155" stroke="#FBBF7C" stroke-width="7" stroke-linecap="round"/>
  <rect x="12" y="186" width="9" height="30" rx="4" fill="#9B30D0"/>
  <rect x="23" y="186" width="9" height="30" rx="4" fill="#9B30D0"/>
  <rect x="188" y="155" width="22" height="34" rx="8" fill="#FF6B9D"/>
  <circle cx="199" cy="145" r="14" fill="#FBBF7C"/>
  <path d="M185 142 Q199 130 213 142" fill="#E8C84A"/>
  <circle cx="195" cy="145" r="2" fill="#333"/>
  <circle cx="203" cy="145" r="2" fill="#333"/>
  <path d="M195 150 Q199 155 203 150" stroke="#333" stroke-width="1.5" fill="none" stroke-linecap="round"/>
  <path d="M210 163 Q222 148 225 138" stroke="#FBBF7C" stroke-width="7" stroke-linecap="round"/>
  <path d="M188 163 Q174 158 163 155" stroke="#FBBF7C" stroke-width="7" stroke-linecap="round"/>
  <rect x="190" y="186" width="9" height="30" rx="4" fill="#9B30D0"/>
  <rect x="201" y="186" width="9" height="30" rx="4" fill="#9B30D0"/>
  <rect class="confetti-bit" x="95" y="75" width="5" height="8" rx="2" fill="#FFD93D" style="animation-delay:.2s"/>
  <rect class="confetti-bit" x="118" y="70" width="6" height="6" rx="2" fill="#C56CF0" style="animation-delay:.5s"/>
  <rect class="confetti-bit" x="130" y="78" width="5" height="7" rx="2" fill="#4FC3F7" style="animation-delay:.8s"/>
</svg>`;

const cards = [
    {
        id: 1,
        title: 'Party with Friends',
        desc: 'Happy Birthday, Sir Tolits! Wishing you a day filled with joy and a year ahead full of continued success. Thank you for your leadership and for being an inspiration to all of us. May you have a wonderful celebration!',
        svg: svg1,
        accent: '#FFD93D',
        tag: '🎁 Gifts & Fun'
    },
    {
        id: 2,
        title: 'Birthday Surprise',
        desc: 'Happy Birthday, Sir Tolits! Enjoy your special day to the fullest. You deserve all the cake and relaxation today! Looking forward to celebrating many more milestones together. Cheers!',
        svg: svg2,
        accent: '#FF6B9D',
        tag: '🎂 Cake Time'
    },
    {
        id: 3,
        title: 'Birthday Celebration',
        desc: 'A very Happy Birthday, Sir Tolits! May this special day bring you as much happiness as you bring to those around you. We appreciate your guidance and support. Cheers to good health and more blessings!',
        svg: svg3,
        accent: '#C56CF0',
        tag: '✨ Celebrations'
    }
];

const currentIndex = ref(0);
const direction = ref('right');
const isAnimating = ref(false);
const showParticles = ref(false);

const currentCard = computed(() => cards[currentIndex.value]);

const particles = ref([]);

const generateParticles = () => {
    particles.value = Array.from({ length: 20 }, (_, i) => ({
        id: i,
        x: Math.random() * 100,
        delay: Math.random() * 1.5,
        duration: 2 + Math.random() * 2,
        size: 4 + Math.random() * 8,
        color: ['#FFD93D', '#FF6B9D', '#C56CF0', '#4FC3F7', '#FF8FB3'][Math.floor(Math.random() * 5)]
    }));
};

onMounted(() => {
    generateParticles();
    showParticles.value = true;
});

const navigate = (dir) => {
    if (isAnimating.value) return;
    isAnimating.value = true;
    direction.value = dir;
    generateParticles();

    if (dir === 'right') {
        currentIndex.value = (currentIndex.value + 1) % cards.length;
    } else {
        currentIndex.value = (currentIndex.value - 1 + cards.length) % cards.length;
    }

    setTimeout(() => { isAnimating.value = false; }, 500);
};

const goTo = (idx) => {
    if (idx === currentIndex.value || isAnimating.value) return;
    direction.value = idx > currentIndex.value ? 'right' : 'left';
    isAnimating.value = true;
    currentIndex.value = idx;
    generateParticles();
    setTimeout(() => { isAnimating.value = false; }, 500);
};
</script>

<template>
    <div class="scene">
        <!-- Ambient orbs -->
        <div class="orb orb-1"></div>
        <div class="orb orb-2"></div>
        <div class="orb orb-3"></div>

        <!-- Floating particles -->
        <div class="particles">
            <div v-for="p in particles" :key="p.id" class="particle" :style="{
                left: p.x + '%',
                width: p.size + 'px',
                height: p.size + 'px',
                background: p.color,
                animationDelay: p.delay + 's',
                animationDuration: p.duration + 's'
            }"></div>
        </div>

        <!-- Header -->
        <div class="header">
            <div class="header-eyebrow">🎉 Special Occasion</div>
            <h1 class="header-title">
                <span class="title-line-1">Birthday Celebration</span>
                <span class="title-divider">of</span>
                <span class="title-name">Sir Tolits</span>
            </h1>
        </div>

        <!-- Main card area -->
        <div class="stage">
            <button class="nav-btn nav-left" @click="navigate('left')" :disabled="isAnimating">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                    <path d="M15 18l-6-6 6-6" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" />
                </svg>
            </button>

            <div class="card-viewport">
                <Transition :name="direction === 'right' ? 'slide-right' : 'slide-left'" mode="out-in">
                    <div :key="currentCard.id" class="card-wrapper">
                        <div class="bday-card" :style="{ '--accent': currentCard.accent }">

                            <!-- Card glow -->
                            <div class="card-glow" :style="{ background: currentCard.accent }"></div>

                            <!-- Tag -->
                            <div class="card-tag">{{ currentCard.tag }}</div>

                            <!-- Illustration -->
                            <div class="illus" v-html="currentCard.svg"></div>

                            <!-- Content -->
                            <div class="card-content">
                                <h3 class="card-title">{{ currentCard.title }}</h3>
                                <div class="card-divider">
                                    <span :style="{ background: currentCard.accent }"></span>
                                </div>
                                <p class="card-desc">{{ currentCard.desc }}</p>

                                <!-- Signature -->
                                <div class="card-footer">
                                    <span class="heart-icon">♥</span>
                                    <span class="from-text">With love & gratitude</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </Transition>
            </div>

            <button class="nav-btn nav-right" @click="navigate('right')" :disabled="isAnimating">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                    <path d="M9 18l6-6-6-6" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" />
                </svg>
            </button>
        </div>

        <!-- Dot indicators -->
        <div class="dots">
            <button v-for="(c, i) in cards" :key="i" class="dot" :class="{ active: i === currentIndex }" @click="goTo(i)" :style="i === currentIndex ? { background: currentCard.accent, boxShadow: `0 0 12px ${currentCard.accent}` } : {}"></button>
        </div>

        <!-- Card counter -->
        <div class="counter">{{ currentIndex + 1 }} / {{ cards.length }}</div>
    </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=DM+Sans:wght@300;400;500&display=swap');

:root {
    --purple-deep: #3A0A6E;
    --purple-dark: #6B21C8;
    --purple-mid: #9B30D0;
    --purple-light: #C56CF0;
    --pink: #FF6B9D;
    --yellow: #FFD93D;
    --blue: #4FC3F7;
    --white: #ffffff;
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: 'DM Sans', sans-serif;
    background: #1A0533;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
    overflow: hidden;
}

/* ---- Scene ---- */
.scene {
    position: relative;
    width: 100%;
    max-width: 520px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0;
    z-index: 1;
}

/* ---- Ambient orbs ---- */
.orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(80px);
    opacity: 0.35;
    pointer-events: none;
    animation: floatOrb 8s ease-in-out infinite;
}

.orb-1 {
    width: 400px;
    height: 400px;
    background: radial-gradient(circle, #9B30D0, transparent 70%);
    top: -100px;
    left: -100px;
    animation-delay: 0s;
}

.orb-2 {
    width: 350px;
    height: 350px;
    background: radial-gradient(circle, #FF6B9D, transparent 70%);
    bottom: -80px;
    right: -80px;
    animation-delay: -3s;
}

.orb-3 {
    width: 300px;
    height: 300px;
    background: radial-gradient(circle, #FFD93D, transparent 70%);
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    opacity: 0.15;
    animation-delay: -6s;
}

@keyframes floatOrb {

    0%,
    100% {
        transform: translate(0, 0);
    }

    33% {
        transform: translate(20px, -20px);
    }

    66% {
        transform: translate(-15px, 15px);
    }
}

/* ---- Particles ---- */
.particles {
    position: fixed;
    inset: 0;
    pointer-events: none;
    overflow: hidden;
}

.particle {
    position: absolute;
    top: -20px;
    border-radius: 3px;
    animation: particleFall linear infinite;
    opacity: 0.8;
}

@keyframes particleFall {
    0% {
        transform: translateY(-20px) rotate(0deg);
        opacity: 0;
    }

    10% {
        opacity: 0.8;
    }

    90% {
        opacity: 0.6;
    }

    100% {
        transform: translateY(100vh) rotate(360deg);
        opacity: 0;
    }
}

/* ---- Header ---- */
.header {
    text-align: center;
    margin-bottom: 28px;
    animation: fadeDown 0.8s ease both;
}

.header-eyebrow {
    font-family: 'DM Sans', sans-serif;
    font-size: 0.7rem;
    font-weight: 500;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: rgba(255, 255, 255, 0.5);
    margin-bottom: 10px;
}

.header-title {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2px;
}

.title-line-1 {
    font-family: 'DM Sans', sans-serif;
    font-size: 0.85rem;
    font-weight: 300;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: rgba(255, 255, 255, 0.6);
}

.title-divider {
    font-family: 'Playfair Display', serif;
    font-size: 0.8rem;
    font-style: italic;
    color: rgba(255, 255, 255, 0.35);
    letter-spacing: 2px;
}

.title-name {
    font-family: 'Playfair Display', serif;
    font-size: 2.4rem;
    font-weight: 900;
    color: #fff;
    letter-spacing: -1px;
    line-height: 1;
    background: linear-gradient(135deg, #fff 0%, #FFD93D 50%, #FF6B9D 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

/* ---- Stage ---- */
.stage {
    width: 100%;
    display: flex;
    align-items: center;
    gap: 12px;
}

/* ---- Card viewport ---- */
.card-viewport {
    flex: 1;
    overflow: hidden;
    position: relative;
}

.card-wrapper {
    display: flex;
    justify-content: center;
}

/* ---- Card ---- */
.bday-card {
    background: rgba(255, 255, 255, 0.97);
    border-radius: 28px;
    width: 100%;
    max-width: 360px;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 24px 22px 20px;
    position: relative;
    overflow: hidden;
    box-shadow:
        0 2px 0 rgba(255, 255, 255, 0.1) inset,
        0 30px 70px rgba(0, 0, 0, 0.5),
        0 0 0 1px rgba(255, 255, 255, 0.08);
    transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.bday-card:hover {
    transform: translateY(-6px) scale(1.015);
}

.card-glow {
    position: absolute;
    top: -60px;
    left: 50%;
    transform: translateX(-50%);
    width: 200px;
    height: 200px;
    border-radius: 50%;
    opacity: 0.15;
    filter: blur(40px);
    pointer-events: none;
    transition: background 0.4s;
}

/* ---- Card tag ---- */
.card-tag {
    align-self: flex-start;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.65rem;
    font-weight: 500;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--accent, #9B30D0);
    background: color-mix(in srgb, var(--accent, #9B30D0) 10%, transparent);
    border: 1px solid color-mix(in srgb, var(--accent, #9B30D0) 25%, transparent);
    padding: 4px 10px;
    border-radius: 20px;
    margin-bottom: 8px;
}

/* ---- Illustration ---- */
.illus {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 4px 0 8px;
}

.illus svg {
    width: 180px;
    height: auto;
    filter: drop-shadow(0 12px 24px rgba(0, 0, 0, 0.12));
}

/* ---- Card content ---- */
.card-content {
    width: 100%;
    text-align: center;
}

.card-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.3rem;
    font-weight: 700;
    color: #1a0533;
    margin-bottom: 10px;
}

.card-divider {
    display: flex;
    justify-content: center;
    margin-bottom: 12px;
}

.card-divider span {
    display: block;
    width: 40px;
    height: 3px;
    border-radius: 2px;
    transition: background 0.4s;
}

.card-desc {
    font-family: 'DM Sans', sans-serif;
    font-size: 0.875rem;
    color: #555;
    line-height: 1.7;
    font-weight: 400;
}

.card-footer {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 6px;
    margin-top: 14px;
    padding-top: 12px;
    border-top: 1px solid #f0e8ff;
}

.heart-icon {
    font-size: 0.9rem;
    color: var(--accent, #FF6B9D);
    transition: color 0.4s;
}

.from-text {
    font-family: 'Playfair Display', serif;
    font-size: 0.7rem;
    font-style: italic;
    color: #aaa;
    letter-spacing: 0.5px;
}

/* ---- Nav buttons ---- */
.nav-btn {
    flex-shrink: 0;
    width: 44px;
    height: 44px;
    border-radius: 50%;
    border: 1px solid rgba(255, 255, 255, 0.15);
    background: rgba(255, 255, 255, 0.07);
    color: rgba(255, 255, 255, 0.8);
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.2s ease;
    backdrop-filter: blur(10px);
}

.nav-btn:hover:not(:disabled) {
    background: rgba(255, 255, 255, 0.18);
    border-color: rgba(255, 255, 255, 0.3);
    transform: scale(1.08);
    color: #fff;
}

.nav-btn:disabled {
    opacity: 0.4;
    cursor: not-allowed;
}

/* ---- Dots ---- */
.dots {
    display: flex;
    gap: 8px;
    margin-top: 20px;
    justify-content: center;
}

.dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.2);
    border: none;
    cursor: pointer;
    transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
    padding: 0;
}

.dot.active {
    width: 24px;
    border-radius: 4px;
}

/* ---- Counter ---- */
.counter {
    font-family: 'DM Sans', sans-serif;
    font-size: 0.65rem;
    letter-spacing: 3px;
    color: rgba(255, 255, 255, 0.25);
    margin-top: 10px;
    text-transform: uppercase;
}

/* ---- Transitions ---- */
.slide-right-enter-active,
.slide-right-leave-active,
.slide-left-enter-active,
.slide-left-leave-active {
    transition: all 0.45s cubic-bezier(0.4, 0, 0.2, 1);
}

.slide-right-enter-from {
    transform: translateX(60px);
    opacity: 0;
}

.slide-right-leave-to {
    transform: translateX(-60px);
    opacity: 0;
}

.slide-left-enter-from {
    transform: translateX(-60px);
    opacity: 0;
}

.slide-left-leave-to {
    transform: translateX(60px);
    opacity: 0;
}

/* ---- SVG animations ---- */
.confetti-bit {
    animation: confettiFall 2.5s ease-in-out infinite;
}

@keyframes confettiFall {

    0%,
    100% {
        transform: translateY(0) rotate(0deg);
        opacity: 1;
    }

    50% {
        transform: translateY(-8px) rotate(20deg);
        opacity: 0.7;
    }
}

.bounce-person {
    animation: bounce 1.4s ease-in-out infinite;
}

@keyframes bounce {

    0%,
    100% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-12px);
    }
}

.twinkle {
    animation: twinkle 1.8s ease-in-out infinite;
}

@keyframes twinkle {

    0%,
    100% {
        opacity: 1;
        transform: scale(1);
    }

    50% {
        opacity: 0.3;
        transform: scale(0.6);
    }
}

@keyframes fadeDown {
    from {
        opacity: 0;
        transform: translateY(-20px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* ---- Responsive ---- */
@media (max-width: 480px) {
    .title-name {
        font-size: 1.9rem;
    }

    .bday-card {
        padding: 20px 16px 16px;
    }

    .nav-btn {
        width: 38px;
        height: 38px;
    }

    .illus svg {
        width: 150px;
    }
}
</style>