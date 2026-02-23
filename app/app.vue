<template>
  <div>
    <NuxtRouteAnnouncer />
    <NuxtPage/>
  </div>
</template>

<script setup>
  import gsap from "gsap";
import {ScrollTrigger, SplitText} from "gsap/all"

  gsap.registerPlugin(ScrollTrigger, SplitText); 

</script>
