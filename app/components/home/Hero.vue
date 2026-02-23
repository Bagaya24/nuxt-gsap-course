<template>
  <section id="hero" class="noisy" :ref="main">
    <h1 class="title">
        Mojito
    </h1>
    <img src="/images/hero-left-leaf.png" alt="Left Leaf" class="left-leaf"/>
    <img src="/images/hero-right-leaf.png" alt="Right Leaf" class="right-leaf"/>

    <div class="body">
        <div class="content">
            <div class="hidden space-y-5 md:block">
                <p>
                    Cool. Crisp. Classic
                </p>
                <p class="subtitle">
                    Sip the spirit <br> of summer
                </p>
            </div>
            <div class="view-cocktails">
                <p class="subtitle">
                    Lorem ipsum dolor sit amet consectetur adipisicing elit. Ab excepturi, adipisci ducimus veniam necessitatibus alias possimus ut totam earum fugiat. Nostrum aperiam nihil veniam quam quasi, animi quisquam voluptatum alias.
                </p>
                <NuxtLink to="/cocktails" >
                    View Cocktails
                </NuxtLink>
            </div>
        </div>
    </div>
  </section>
</template>

<script setup>

import gsap from "gsap";
import { SplitText } from "gsap/SplitText";

const main = ref(null);
let ctx;
onMounted(() => {
    ctx = gsap.context(() => {
        const heroSplit = new SplitText(".title", { type: "chars, words"});
        const paragraphtSplit =new  SplitText(".subtitle", {type: "lines"});

        heroSplit.chars.forEach((char) => char.classList.add("text-gradient"));
        gsap.from(heroSplit.chars, {
            yPercent: 100,
            duration: 1.8,
            ease: "expo.out",
            stagger: 0.06
        });

        gsap.from(paragraphtSplit.lines, {
            opacity:0,
            yPercent: 100,
            duration: 1.8,
            ease: "expo.out",
            stagger: 0.02, 
            delay: 0.5
        });

        gsap.timeline({
            scrollTrigger: {
                trigger: "#hero",
                start: "top top",
                end: "bottom top",
                scrub: true,
            }
        })
        .to(".left-leaf", {
            y: -300,
        }, 0)
        .to(".right-leaf", {
            y: 500,
        }, 0);
    }, main.value);
});

onUnmounted(() => {
    if(ctx) ctx.revert();
});
</script>