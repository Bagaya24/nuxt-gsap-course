<template>
    <!-- On ajoute la ref pour GSAP -->
    <nav ref="navbar" class="fixed top-0 w-full z-50"> 
        <div>
            <NuxtLink to="/" class="flex items-center gap-2">
                <img src="/images/logo.png" alt="logo">
                Velvet Pour
            </NuxtLink>
        </div>
        <ul>
            <li v-for="link in navLinks" :key="link.id">
                <a :href="`#${link.id}`">{{ link.title }}</a>
            </li>
        </ul>
    </nav>
</template>

<script setup>
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

// On enregistre le plugin (important !)
gsap.registerPlugin(ScrollTrigger);

const navbar = ref(null);
let ctx;

onMounted(() => {
    // On n'exécute le code que côté client
    ctx = gsap.context(() => {
        const navTween = gsap.timeline({
            scrollTrigger: {
                trigger: navbar.value, // Utilisation de la ref
                start: "top top",      // Commence dès que le top du nav touche le top de l'écran
                toggleActions: "play none none reverse", // Anime au retour
                scrub: true,           // Optionnel: lie l'anim au défilement
            }
        });

        navTween.to(navbar.value, {
            backgroundColor: "rgba(0, 0, 0, 0.5)", // Notation standard CSS
            backdropFilter: "blur(10px)",         // Correction: c'est backdrop-filter
            duration: 1,
            ease: "power2.inOut"
        });
    }, navbar.value);
});

// Très important : Nettoyer GSAP quand on change de page
onUnmounted(() => {
    if (ctx) ctx.revert();
});
</script>
