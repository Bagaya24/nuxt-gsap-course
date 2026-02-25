<template>
  <div id="art" ref="main">
    <div class="container mx-auto h-full pt-20">
      <h2 class="will-fade">The ART</h2>

      <div class="content">
        <ul class="space-y-4 will-fade">
          <li
            v-for="feature in goodLists"
            :key="feature"
            class="flex items-center gap-2"
          >
            <img src="/images/check.png" alt="check" />
            <p>{{ feature }}</p>
          </li>
        </ul>

        <div class="cocktail-img">
          <img
            src="/images/under-img.jpg"
            alt="cocktail"
            class="abs-center masked-img size-full object-contain"
          />
        </div>

        <ul class="space-y-4 will-fade">
          <li
            v-for="feature in featureLists"
            :key="feature"
            class="flex items-center justify-start gap-2"
          >
            <img src="/images/check.png" alt="check" />
            <p class="md:w-fit w-60">{{ feature }}</p>
          </li>
        </ul>
      </div>

      <div class="masked-container">
        <h2 class="will-fade">Sip-Worthy Perfection</h2>
        <div class="masked-conten">
          <h3>Made with Craft, Poured with Passion</h3>
          <p>
            This isn't just a drink. It's a carefully moment made just for you
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { goodLists, featureLists } from "../../utils/index";
import gsap from "gsap";

const main = ref(null);
const { isMobile } = useDevice();
let ctx;

onMounted(() => {
  const start = isMobile ? "top 20%" : "top top";

  ctx = gsap.context(() => {
    const maskTimeline = gsap.timeline({
      scrollTrigger: {
        trigger: main.value,
        start: start,
        end: "bottom center",
        scrub: 1.5,
        pin: true,
      },
    });

    maskTimeline.to(".will-fade", {
      opacity: 0,
      stagger: 0.2,
      ease: "power1.inOut",
    })
    .to('.masked-img', {
        scale: 1.3,
        maskPosition: 'center', maskSize: '400%', duration: 2, ease: "power1.inOut"
    })
    .to('.masked-conten', {
        opacity: 1, duration: 1, ease: "power1.inOut"
    }, '-=0.5');
  }, main.value);
});

onUnmounted(() => {
  if (ctx) ctx.revert();
});
</script>
