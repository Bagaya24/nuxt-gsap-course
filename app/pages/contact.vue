<template>
    <footer id="contact" ref="main">
        <!-- <img src="/images/footer-right-leaf.png" alt="leaf-right" id="f-right-leaf "> -->
        <img src="/images/footer-left-leaf.png" alt="leaf-left" id="f-left-leaf">
        
        <div class="content">
            <h2>
                Where to find us
            </h2>
            <div>
                <h3>Visit Our Bar</h3>
        <p>Q. Les volcans, rue du Manguier, N°38</p>
            </div>

            <div>
                <h3>Contact Us</h3>
                <p>+243 99 99 99 99</p>
                <p>contact@kivu.com</p>
            </div>

            <div>
                <h3>Open Every Day</h3>
                <p v-for="time in openingHours" :key="time.time">
                    {{ time.day }}: {{ time.time }}
                </p>
            </div>

            <div>
                <h3>Socials</h3>
                <div class="flex-center gap-5">
                    <NuxtLink v-for="social in socials" :key="social.name" :to="social.url" target="_blank" :aria-label="social.name">
                        <img :src="social.icon" :alt="social.name" class="w-6 h-6 object-contain">

                    </NuxtLink>
                </div>
            </div>
        </div>
        
        
    </footer>
</template>

<script setup>
import gsap from 'gsap';
import { SplitText } from 'gsap/SplitText';

const main = ref(null);
let ctx;

onMounted(() => {
    ctx = gsap.context(() => {
        const titleSplit = SplitText.create('#contact h2', { type: 'words' });

        const scrollTimeline = gsap.timeline({
            scrollTrigger: {
                trigger: main.value,
                start: 'top center',
            },
            ease: "power1.inOut"
        });

        scrollTimeline
        .from(titleSplit.words, {
            opacity: 0, yPercent: 100, stagger: 0.02
        })
        .from('#contact h3, #contact p', {
            opacity: 0, yPercent: 100, stagger: 0.02
        })
        .to('#f-left-leaf', {
            y: -50, duration: 1, ease: "power1.inOut"
        }, '<');
        }, main.value)
});

onUnmounted(() => {
    if (ctx) ctx.revert();
})

</script>