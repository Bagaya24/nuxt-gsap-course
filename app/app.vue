<template>
  <div>
    <NuxtRouteAnnouncer />
    <NuxtLayout/>
     <NuxtPage/>
  </div>
</template>

<script setup>

useHead({
  title: "Velvet Pour",
  link: [
    {
      rel: "icon",
      type: "image/png",
      href: "/images/logo.png",
    },
  ],
  meta: [
    {
      name: "description",
      content: "A modern library management system built with Nuxt 3 and GSAP.",
    },
  ],
});
</script>
