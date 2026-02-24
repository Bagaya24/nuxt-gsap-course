<template>
    <section id="menu" aria-labelledby="menu-heading" ref="main">
        <img src="/images/slider-left-leaf.png" alt="left-lead" id="m-left-leaf">
        <img src="/images/slider-right-leaf.png" alt="right-lead" id="m-right-leaf">

        <h2 id="menu-heading" class="sr-only">
            Cocktail Menu 
        </h2>

        <nav class="cocktail-tabs" aria-label="Cocktail Navigation">
            <button 
            v-for=" (cocktail, index) in sliderLists" 
            :key="cocktail.id" 
            :class="`${index === currentIndex ? 'text-white border-white' : 'text-white/50 border-white/50'}`"
            @click="gotoSlide(index)"
            >
                {{ cocktail.name }}
            </button>
        </nav>

        <div class="content">
            <div class="arrows">
                <button 
                class="text-left"
                @click="gotoSlide(currentIndex -1)"
                >
                <span>{{prevCocktail.name}}</span>
                <img src="/images/right-arrow.png" alt="right arrow" aria-hidden="true" >
                </button>

                <button 
                class="text-left"
                @click="gotoSlide(currentIndex + 1)"
                >
                <span>{{nextCocktail.name}}</span>
                <img src="/images/left-arrow.png" alt="left arrow" aria-hidden="true" >
                </button>
            </div>
            
            <div class="cocktail">
                <img :src="currentCocktail.image" :alt="currentCocktail.name" class="objet-contain">
            </div>
            <div class="recipe">
                <div ref="contentRef" class="info">
                    <p id="title">{{ currentCocktail.name }}</p>
                </div>
                <div class="details">
                    <h2>
                        {{ currentCocktail.title }}
                    </h2>
                    <p>{{ currentCocktail.description }}</p>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import gsap from 'gsap';

const main = ref(null);
const currentIndex = ref(0);
const contentRef = ref(null);
let ctx;
const totalCocktails = sliderLists.length;

const gotoSlide = (index) => {
    const newIndex = (index + totalCocktails) % totalCocktails;
    currentIndex.value = newIndex;
};

const getCocktailAt = (indexOffset) => {
    return sliderLists[(currentIndex.value + indexOffset + totalCocktails) % totalCocktails];
};

const currentCocktail = computed(() => getCocktailAt(0));
const nextCocktail = computed(() => getCocktailAt(1));
const prevCocktail = computed(() => getCocktailAt(-1));


const createAnimation = () => {
    if (ctx) ctx.revert();

    ctx = gsap.context(() => {
        gsap.fromTo('#title',{opacity: 0}, {opacity: 1, duration: 1});
        gsap.fromTo('.cocktail img', {opacity: 0, xPercent: -100},
            {xPercent: 0, opacity: 1, duration: 1, ease: 'power1.inOut'})
         gsap.fromTo('.details h2', {opacity: 0, yPercent: 100},
            {yPercent: 0, opacity: 1, duration: 1, ease: 'power1.inOut'});
        gsap.fromTo('.details p', {opacity: 0, yPercent: 100},
            {yPercent: 0, opacity: 1, duration: 1, ease: 'power1.inOut'});
    }, main.value)
};

watch(() => currentIndex.value, () => {
    createAnimation();
});

</script>