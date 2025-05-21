<script lang="ts">
  // Import components
  import Header from "./lib/Header.svelte";
  import Hero from "./lib/Hero.svelte";
  import Menu from "./lib/Menu.svelte";
  import Info from "./lib/Info.svelte";
  import About from "./lib/About.svelte";
  import Footer from "./lib/Footer.svelte";

  // Sections for navigation
  const sections = [
    { id: "menu", label: "Menu" },
    { id: "info", label: "Info" },
    { id: "about", label: "About" },
  ];
</script>

<Header {sections} />

<main>
  <Hero />
  <Menu />
  <Info />
  <About />
</main>

<Footer />

<style>
  main {
    width: 100%;
  }
</style>
