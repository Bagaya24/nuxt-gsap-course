<template>
  <div ref="main">
    <section id="hero" class="noisy">
      <h1 class="title">Mojito</h1>
      <img src="/images/hero-left-leaf.png" alt="Left Leaf" class="left-leaf" />
      <img
        src="/images/hero-right-leaf.png"
        alt="Right Leaf"
        class="right-leaf"
      />

      <div class="body">
        <div class="content">
          <div class="hidden space-y-5 md:block">
            <p>Cool. Crisp. Classic</p>
            <p class="subtitle">
              Sip the spirit <br />
              of summer
            </p>
          </div>
          <div class="view-cocktails">
            <p class="subtitle">
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Ab
              excepturi, adipisci ducimus veniam necessitatibus alias possimus
              ut totam earum fugiat. Nostrum aperiam nihil veniam quam quasi,
              animi quisquam voluptatum alias.
            </p>
            <NuxtLink to="/cocktails"> View Cocktails </NuxtLink>
          </div>
        </div>
      </div>
    </section>
    <div class="video absolute inset-0">
      <video
        src="/videos/output.mp4"
        muted
        playsinline
        preload="auto"
        ref="videoRef"
      />
    </div>
  </div>
</template>

<script setup>
import gsap from "gsap";
import { SplitText } from "gsap/SplitText";

const main = ref(null);
const videoRef = ref(null);
const { isMobile } = useDevice();
let ctx;

onMounted(() => {
  ctx = gsap.context(() => {
    const heroSplit = new SplitText(".title", { type: "chars, words" });
    const paragraphtSplit = new SplitText(".subtitle", { type: "lines" });

    heroSplit.chars.forEach((char) => char.classList.add("text-gradient"));
    gsap.from(heroSplit.chars, {
      yPercent: 100,
      duration: 1.8,
      ease: "expo.out",
      stagger: 0.06,
    });

    gsap.from(paragraphtSplit.lines, {
      opacity: 0,
      yPercent: 100,
      duration: 1.8,
      ease: "expo.out",
      stagger: 0.02,
      delay: 0.5,
    });

    gsap
      .timeline({
        scrollTrigger: {
          trigger: "#hero",
          start: "top top",
          end: "bottom top",
          scrub: true,
        },
      })
      .to(
        ".left-leaf",
        {
          y: -300,
        },
        0,
      )
      .to(
        ".right-leaf",
        {
          y: 500,
        },
        0,
      );

    const startValue = isMobile ? "top 50%" : "center 60%";
    const endValue = isMobile ? "120% top" : "+=1000";

    const videoTimeline = gsap.timeline({
      scrollTrigger: {
        trigger: videoRef.value,
        start: startValue,
        end: endValue,
        scrub: true,
        pin: true,
      },
    });

    if (videoRef.value) {
      const initTimeLine = () => {
        videoTimeline.to(videoRef.value, {
          currentTime: videoRef.value.duration,
          ease: "none",
        });
      };
      if (videoRef.value.readyState >= 1) {
        initTimeLine();
      } else {
        videoRef.value.onloadedmetadata = initTimeLine;
      }
    }
  }, main.value);
});

onUnmounted(() => {
  if (ctx) ctx.revert();
});
</script>
