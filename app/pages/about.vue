<template>
  <div id="about" ref="main">
    <div class="mb-16 md:px-0 px-5">
      <div class="content">
        <div class="md:col-span-8">
          <p class="badge">Best Cocktails</p>
          <h2>
            Where every detail matters <span class="text-white">-</span>
            from muddle to garnish
          </h2>
        </div>
        <div class="sub-content">
          <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Iure,
            necessitatibus corrupti nulla ducimus earum error ad. Nesciunt,
            commodi animi eaque quisquam illum sapiente ad, quia, repudiandae
            nulla laudantium enim. Fugiat!
          </p>
          <div>
            <p class="md:text-3xl text-xl font-bold"><span>4.5</span>/5</p>
            <p class="text-sm text-white-100">More than 12000 customers</p>
          </div>
        </div>
      </div>
    </div>

    <div class="top-grid">
      <div class="md:col-span-3">
        <div class="noisy">
          <img src="/images/abt1.png" alt="grid-image-1" />
        </div>
      </div>

      <div class="md:col-span-6">
        <div class="noisy">
          <img src="/images/abt2.png" alt="grid-image-2" />
        </div>
      </div>

      <div class="md:col-span-3">
        <div class="noisy">
          <img src="/images/abt5.png" alt="grid-image-3" />
        </div>
      </div>
    </div>

    <div class="bottom-grid">
      <div class="md:col-span-8">
        <div class="noisy">
          <img src="/images/abt3.png" alt="grid-image-3" />
        </div>
      </div>

      <div class="md:col-span-4">
        <div class="noisy">
          <img src="/images/abt4.png" alt="grid-image-4" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
    import gsap from 'gsap';
    import { SplitText } from 'gsap/SplitText';

    const main = ref(null);
    onMounted(() => {
        const titleSplit = SplitText.create('#about h2', { type: 'words' });

        const scrollTimeline = gsap.timeline({
            scrollTrigger: {
                trigger: main.value,
                start: 'top center',
            }
        });

        scrollTimeline.from(titleSplit.words, {
            opacity: 0,
            duration: 1, 
            yPercent: 100,
            ease: "expor.out",
            stagger: 0.02
        })
        .from(".top-grid div, .bottom-grid div", {
            opacity: 0,
            duration: 1,
            ease: "power1.inOut",
            stagger: 0.04, 
        }, '-=0.5');
    })
</script>