<template>
    <section id="cocktails" class="noisy" ref="cocktails">
        <img src="/images/cocktail-left-leaf.png" alt="Left Leaf" id="c-left-leaf">
        <img src="/images/cocktail-right-leaf.png" alt="Right Leaf" id="c-right-leaf">

        <div class="list">
            <div class="popular">
                <h2>Most popular cocktails:</h2>
                <ul>
                    <li v-for=" {name, price, country, detail} in cocktailLists" :key="name">
                        <div class="md:me-28">
                            <h3>{{ name }}</h3>
                            <p>{{ country }} | {{ detail }}</p>
                        </div>
                        <span>- {{ price }}</span>
                    </li>
                </ul>
            </div>

            <div class="loved">
                <h2>Most loved mocktails:</h2>
                <ul>
                    <li v-for=" {name, price, country, detail} in mockTailLists" :key="name">
                        <div class="me-28">
                            <h3>{{ name }}</h3>
                            <p>{{ country }} | {{ detail }}</p>
                        </div>
                        <span>- {{ price }}</span>
                    </li>
                </ul>
            </div>
        </div>
    </section>
</template>

<script setup>
import gsap from 'gsap'

const cocktails = ref();

onMounted(() => {
    const parallaxTimeline = gsap.timeline({
        scrollTrigger: {
            trigger: cocktails.value,
            start: 'top 30%',
            end: 'bottom 80%',
            scrub: true
        }
    });
    parallaxTimeline.from('#c-left-leaf', { y: 100, x: -150 })
                    .from('#c-right-leaf', { y: 100, x: 150 }, '-=1');
})
</script>