<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const is_active = ref(true)
const emit = defineEmits(['enterSite'])

/* ─────────── STATE ─────────── */
const splashHidden = ref(false)
const mainVisible = ref(false)

let canvas
let ctx
let pieces = []
let animating = false

/* ─────────── CANVAS FUNCTIONS ─────────── */

function resizeCanvas() {
    if (!canvas) return
    canvas.width = window.innerWidth
    canvas.height = window.innerHeight
}

function spawnConfetti() {
    resizeCanvas()
    pieces = []

    const colors = [
        '#FFD93D', '#FF6B9D', '#4FC3F7',
        '#C56CF0', '#ffffff', '#9B30D0'
    ]

    for (let i = 0; i < 160; i++) {
        pieces.push({
            x: Math.random() * canvas.width,
            y: Math.random() * -canvas.height,
            w: Math.random() * 10 + 5,
            h: Math.random() * 6 + 3,
            color: colors[Math.floor(Math.random() * colors.length)],
            speed: Math.random() * 3 + 2,
            angle: Math.random() * 360,
            spin: (Math.random() - .5) * 6,
            drift: (Math.random() - .5) * 2,
            opacity: 1
        })
    }

    animating = true
    drawConfetti()
}

function drawConfetti() {
    if (!animating) return

    ctx.clearRect(0, 0, canvas.width, canvas.height)

    pieces.forEach(p => {
        p.y += p.speed
        p.x += p.drift
        p.angle += p.spin

        if (p.y > canvas.height * .85) {
            p.opacity -= .025
        }

        ctx.save()
        ctx.globalAlpha = Math.max(0, p.opacity)
        ctx.translate(p.x + p.w / 2, p.y + p.h / 2)
        ctx.rotate(p.angle * Math.PI / 180)
        ctx.fillStyle = p.color
        ctx.fillRect(-p.w / 2, -p.h / 2, p.w, p.h)
        ctx.restore()
    })

    pieces = pieces.filter(p => p.opacity > 0)

    if (pieces.length > 0) {
        requestAnimationFrame(drawConfetti)
    } else {
        animating = false
        ctx.clearRect(0, 0, canvas.width, canvas.height)
    }
}

/* ─────────── METHODS ─────────── */

function enterSite() {
    spawnConfetti()
    splashHidden.value = true

    setTimeout(() => {
        mainVisible.value = true
    }, 600)
}

function enter() {
    emit('enterSite')
    // mainVisible.value = false
    // splashHidden.value = false
}

/* ─────────── LIFECYCLE ─────────── */

onMounted(() => {
    canvas = document.getElementById('confetti-canvas')
    if (canvas) {
        ctx = canvas.getContext('2d')
        resizeCanvas()
        window.addEventListener('resize', resizeCanvas)
    }
})

onBeforeUnmount(() => {
    window.removeEventListener('resize', resizeCanvas)
})
</script>

<template>

    <canvas id="confetti-canvas"></canvas>

    <div class="">

        <div id="splash" :class="{ hide: splashHidden }">

            <svg class="floater" style="top:8%;left:5%;width:50px;animation-delay:0s" viewBox="0 0 60 70" fill="none">
                <ellipse cx="30" cy="30" rx="18" ry="22" fill="#FFD93D" />
                <line x1="30" y1="52" x2="33" y2="70" stroke="#FFD93D" stroke-width="2" />
            </svg>
            <svg class="floater" style="top:6%;right:8%;width:44px;animation-delay:1.2s" viewBox="0 0 60 70" fill="none">
                <ellipse cx="30" cy="30" rx="18" ry="22" fill="#FF6B9D" />
                <line x1="30" y1="52" x2="27" y2="70" stroke="#FF6B9D" stroke-width="2" />
            </svg>
            <svg class="floater" style="top:15%;left:15%;width:36px;animation-delay:2s" viewBox="0 0 60 70" fill="none">
                <ellipse cx="30" cy="30" rx="18" ry="22" fill="#4FC3F7" />
                <line x1="30" y1="52" x2="32" y2="70" stroke="#4FC3F7" stroke-width="2" />
            </svg>
            <svg class="floater" style="bottom:12%;right:12%;width:42px;animation-delay:.7s" viewBox="0 0 60 70" fill="none">
                <ellipse cx="30" cy="30" rx="18" ry="22" fill="#C56CF0" />
                <line x1="30" y1="52" x2="28" y2="70" stroke="#C56CF0" stroke-width="2" />
            </svg>
            <svg class="floater" style="bottom:18%;left:8%;width:38px;animation-delay:1.8s" viewBox="0 0 60 70" fill="none">
                <ellipse cx="30" cy="30" rx="18" ry="22" fill="#FFD93D" />
                <line x1="30" y1="52" x2="31" y2="70" stroke="#FFD93D" stroke-width="2" />
            </svg>

            <div class="splash-inner">

                <div class="cake-wrap">
                    <svg viewBox="0 0 200 160" width="200" height="160" fill="none">
                        <rect x="20" y="108" width="160" height="44" rx="22" fill="#FF6B9D" />
                        <rect x="30" y="108" width="140" height="20" rx="10" fill="#FF8FB3" />
                        <ellipse cx="55" cy="108" rx="9" ry="6" fill="#fff" opacity=".6" />
                        <ellipse cx="100" cy="104" rx="11" ry="7" fill="#fff" opacity=".6" />
                        <ellipse cx="148" cy="108" rx="9" ry="6" fill="#fff" opacity=".6" />
                        <rect x="44" y="64" width="112" height="46" rx="18" fill="#9B30D0" />
                        <rect x="54" y="64" width="92" height="20" rx="10" fill="#C56CF0" />
                        <ellipse cx="72" cy="64" rx="8" ry="5" fill="#fff" opacity=".6" />
                        <ellipse cx="100" cy="60" rx="10" ry="6" fill="#fff" opacity=".6" />
                        <ellipse cx="130" cy="64" rx="8" ry="5" fill="#fff" opacity=".6" />
                        <rect x="68" y="30" width="64" height="36" rx="13" fill="#FFD93D" />
                        <rect x="76" y="30" width="48" height="15" rx="7" fill="#FFE770" />
                        <ellipse cx="88" cy="30" rx="6" ry="4" fill="#fff" opacity=".5" />
                        <ellipse cx="100" cy="27" rx="7" ry="5" fill="#fff" opacity=".5" />
                        <ellipse cx="114" cy="30" rx="5" ry="4" fill="#fff" opacity=".5" />
                        <rect x="82" y="12" width="7" height="20" rx="3" fill="#4FC3F7" />
                        <rect x="97" y="8" width="7" height="24" rx="3" fill="#FF6B9D" />
                        <rect x="112" y="12" width="7" height="20" rx="3" fill="#C56CF0" />
                        <ellipse cx="85" cy="10" rx="4" ry="5" fill="#FFD93D" />
                        <ellipse cx="85" cy="9" rx="2" ry="3" fill="#FF6B9D" opacity=".8" />
                        <ellipse cx="100" cy="6" rx="4" ry="5" fill="#FFD93D" />
                        <ellipse cx="100" cy="5" rx="2" ry="3" fill="#FF6B9D" opacity=".8" />
                        <ellipse cx="115" cy="10" rx="4" ry="5" fill="#FFD93D" />
                        <ellipse cx="115" cy="9" rx="2" ry="3" fill="#FF6B9D" opacity=".8" />
                    </svg>
                </div>

                <div class="company-badge">Muramoto / Maple</div>

                <div class="splash-headline">
                    <span class="presents">proudly celebrates</span>
                    <span class="big-text">Happy <em>Birthday!</em></span>
                    <span class="staff-role">🖥️ IT Staff &nbsp;·&nbsp; 6 Years of Excellence</span>
                </div>

                <div>
                    <span class="years-pill">🎉 6 Wonderful Years with Us!</span>
                </div>

                <div>
                    <button class="enter-btn" @click="enterSite">
                        🎂 &nbsp; Let's Celebrate!
                    </button>
                </div>

            </div>
        </div>

        <div id="main-page" :class="{ show: mainVisible }">
            <div class="main-card">

                <div style="font-size:64px;margin-bottom:16px;">🎂</div>

                <h1>Happy <em>Birthday!</em></h1>

                <div class="tag-row">
                    <span class="tag yellow">🖥️ IT Staff</span>
                    <span class="tag pink">🎉 6 Years</span>
                    <span class="tag">Muramoto / Maple</span>
                </div>

                <p>
                    Today, we pause the tickets, silence the alerts, and celebrate the person
                    who keeps everything running behind the scenes. Six years of dedication,
                    patience, and quiet excellence — and we are so grateful for every single one.
                    <br /><br />
                    Wishing you a day as wonderful as you are. 🎈
                </p>

                <button class="enter-btn" @click="enter" style="font-size:13px;padding:10px 28px;">
                    Enter
                </button>

            </div>
        </div>
    </div>
</template>

<style scoped>
:root {
    --purple-dark: #5B1BA8;
    --purple-mid: #9B30D0;
    --pink: #FF6B9D;
    --yellow: #FFD93D;
    --blue: #4FC3F7;
    --cream: #FFF8F0;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Nunito', sans-serif;
    background: linear-gradient(135deg, #5B1BA8 0%, #9B30D0 55%, #C56CF0 100%);
    min-height: 100vh;
    /* overflow: hidden; */
}

/* ── SPLASH SCREEN ── */
#splash {
    position: fixed;
    inset: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    z-index: 100;
    background: linear-gradient(135deg, #5B1BA8 0%, #9B30D0 55%, #C56CF0 100%);
    transition: opacity .8s ease, transform .8s ease;
}

#splash.hide {
    opacity: 0;
    pointer-events: none;
    transform: scale(1.05);
}

/* ── CONFETTI CANVAS ── */
#confetti-canvas {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 99;
}

/* ── SPLASH CONTENT ── */
.splash-inner {
    text-align: center;
    position: relative;
    z-index: 2;
    padding: 20px;
}

/* Cake SVG */
.cake-wrap {
    opacity: 0;
    transform: translateY(40px) scale(.8);
    animation: cakeIn .9s cubic-bezier(.34, 1.56, .64, 1) .3s forwards;
}

@keyframes cakeIn {
    to {
        opacity: 1;
        transform: translateY(0) scale(1);
    }
}

/* Company badge */
.company-badge {
    display: inline-block;
    background: rgba(255, 255, 255, .15);
    border: 1px solid rgba(255, 255, 255, .3);
    color: #fff;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 3px;
    text-transform: uppercase;
    padding: 6px 18px;
    border-radius: 50px;
    opacity: 0;
    animation: fadeUp .6s ease .9s forwards;
    margin-bottom: 16px;
}

/* Main headline */
.splash-headline {
    opacity: 0;
    animation: fadeUp .6s ease 1.1s forwards;
}

.splash-headline .presents {
    display: block;
    font-size: 13px;
    font-weight: 600;
    color: rgba(255, 255, 255, .7);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 8px;
}

.splash-headline .big-text {
    font-family: 'Playfair Display', serif;
    font-size: clamp(38px, 8vw, 72px);
    font-weight: 700;
    color: #fff;
    line-height: 1.1;
    display: block;
}

.splash-headline .big-text em {
    color: var(--yellow);
    font-style: italic;
}

.splash-headline .staff-role {
    display: block;
    font-size: 14px;
    font-weight: 700;
    color: rgba(255, 255, 255, .8);
    letter-spacing: 1px;
    margin-top: 10px;
}

/* Years badge */
.years-pill {
    display: inline-block;
    background: var(--yellow);
    color: #5B1BA8;
    font-size: 13px;
    font-weight: 900;
    padding: 6px 20px;
    border-radius: 50px;
    margin-top: 14px;
    opacity: 0;
    animation: popIn .5s cubic-bezier(.34, 1.56, .64, 1) 1.4s forwards;
}

@keyframes popIn {
    to {
        opacity: 1;
        transform: scale(1);
    }
}

/* Enter button */
.enter-btn {
    display: inline-block;
    margin-top: 36px;
    background: #fff;
    color: var(--purple-dark);
    font-family: 'Nunito', sans-serif;
    font-size: 15px;
    font-weight: 800;
    padding: 14px 44px;
    border-radius: 50px;
    border: none;
    cursor: pointer;
    letter-spacing: .5px;
    opacity: 0;
    animation: fadeUp .6s ease 1.7s forwards;
    box-shadow: 0 8px 30px rgba(0, 0, 0, .25);
    transition: transform .2s, box-shadow .2s;
    text-decoration: none;
}

.enter-btn:hover {
    transform: translateY(-4px) scale(1.04);
    box-shadow: 0 16px 40px rgba(0, 0, 0, .3);
    color: var(--purple-dark);
}

/* Floating decorations */
.floater {
    position: absolute;
    pointer-events: none;
    animation: floatAround 5s ease-in-out infinite;
}

@keyframes floatAround {

    0%,
    100% {
        transform: translateY(0) rotate(0deg);
    }

    50% {
        transform: translateY(-18px) rotate(15deg);
    }
}

/* ── MAIN PAGE (shown after splash) ── */
#main-page {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity .8s ease .3s;
    padding: 40px 20px;
}

#main-page.show {
    opacity: 1;
}

.main-card {
    background: rgba(255, 255, 255, .1);
    backdrop-filter: blur(16px);
    border: 1px solid rgba(255, 255, 255, .2);
    border-radius: 28px;
    max-width: 700px;
    width: 100%;
    padding: 50px 44px;
    text-align: center;
    color: #fff;
}

.main-card h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(28px, 5vw, 48px);
    font-weight: 700;
    margin-bottom: 12px;
}

.main-card h1 em {
    color: var(--yellow);
    font-style: italic;
}

.main-card p {
    font-size: 15px;
    color: rgba(255, 255, 255, .8);
    line-height: 1.8;
    max-width: 500px;
    margin: 0 auto 28px;
}

.tag-row {
    display: flex;
    gap: 12px;
    justify-content: center;
    flex-wrap: wrap;
    margin-bottom: 30px;
}

.tag {
    background: rgba(255, 255, 255, .15);
    border: 1px solid rgba(255, 255, 255, .25);
    border-radius: 50px;
    padding: 6px 18px;
    font-size: 12px;
    font-weight: 700;
    letter-spacing: 1px;
    color: #fff;
}

.tag.yellow {
    background: var(--yellow);
    color: #5B1BA8;
    border-color: var(--yellow);
}

.tag.pink {
    background: var(--pink);
    color: #fff;
    border-color: var(--pink);
}

/* ── HELPERS ── */
@keyframes fadeUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}
</style>