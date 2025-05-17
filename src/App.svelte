<script lang="ts">
  import { onMount } from "svelte";
  import menuData from "./lib/menu.json";
  import blairImage from "./assets/blair.JPEG";

  // Sections for navigation
  const sections = [
    { id: "home", label: "Home" },
    { id: "menu", label: "Menu" },
    { id: "info", label: "Info" },
    { id: "about", label: "About" },
  ];

  // Menu categories based on the requirements
  const menuCategories = [
    { name: "Specialty Drinks", id: "specialties" },
    { name: "Smoothies", id: "smoothies" },
    { name: "Coffee", id: "coffee" },
    { name: "Matcha/Tea", id: "tea" },
  ];

  // State for mobile menu
  let mobileMenuOpen = false;

  // State for expanded menu categories
  let expandedCategories: Record<string, boolean> = {};

  // Initialize all categories as collapsed
  onMount(() => {
    menuCategories.forEach((category) => {
      expandedCategories[category.id] = false;
    });
  });

  // Toggle category expansion
  function toggleCategory(categoryId: string) {
    expandedCategories[categoryId] = !expandedCategories[categoryId];
  }

  // Toggle mobile menu
  function toggleMobileMenu() {
    mobileMenuOpen = !mobileMenuOpen;
  }

  // Close mobile menu when clicking on a link
  function closeMenu() {
    mobileMenuOpen = false;
  }

  // Find menu items for each category
  function getCategoryItems(categoryName: string): any[] {
    if (categoryName === "Specialty Drinks") {
      return (
        (menuData.categories.find((c) => c.name === "Specialties")
          ?.items as any[]) || []
      );
    } else if (categoryName === "Smoothies") {
      return (
        (menuData.categories.find((c) => c.name === "Smoothies")
          ?.items as any[]) || []
      );
    } else if (categoryName === "Coffee") {
      const coffeeItems = menuData.categories
        .filter((c) => ["Espresso", "Cold Brew & Nitro"].includes(c.name))
        .flatMap((c) => c.items as any[]);
      return coffeeItems || [];
    } else if (categoryName === "Matcha/Tea") {
      return (
        (menuData.categories.find((c) => c.name === "Teas")?.items as any[]) ||
        []
      );
    }
    return [];
  }
</script>

<header>
  <div class="container">
    <div class="navbar">
      <div class="logo">
        <a href="#home">Benny's Beanery</a>
      </div>

      <nav class={mobileMenuOpen ? "active" : ""}>
        <ul>
          {#each sections as section}
            <li>
              <a href="#{section.id}" on:click={closeMenu}>{section.label}</a>
            </li>
          {/each}
        </ul>
      </nav>

      <button
        class="hamburger-button"
        on:click={toggleMobileMenu}
        aria-label="Toggle menu"
        aria-expanded={mobileMenuOpen}
      >
        <div class="hamburger">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </button>
    </div>
  </div>
</header>

<main>
  <!-- Hero Section -->
  <section id="home" class="hero">
    <div class="hero-content">
      <h1>Benny's Beanery</h1>
      <p>Crafting perfect coffee experiences since 2020</p>
      <a href="#menu" class="btn">Explore Our Menu</a>
    </div>
  </section>

  <!-- Menu Section -->
  <section id="menu" class="menu-section">
    <div class="container">
      <div class="section-title">
        <h2>Our Menu</h2>
      </div>

      <div class="menu-container">
        {#each menuCategories as category}
          <div class="menu-category">
            <button
              class="category-header"
              on:click={() => toggleCategory(category.id)}
              aria-expanded={expandedCategories[category.id]}
              aria-controls={`category-${category.id}-items`}
            >
              <h3>{category.name}</h3>
              <span class="toggle-icon"
                >{expandedCategories[category.id] ? "−" : "+"}</span
              >
            </button>

            {#if expandedCategories[category.id]}
              <div class="category-items" id={`category-${category.id}-items`}>
                {#each getCategoryItems(category.name) as item}
                  <div class="menu-item">
                    <div class="item-header">
                      <h4>{item.name}</h4>
                      {#if item.prices && item.prices.length > 0}
                        <div class="item-price">
                          ${item.prices[0].toFixed(2)}
                          {#if item.prices.length > 1}
                            - ${item.prices[item.prices.length - 1].toFixed(2)}
                          {/if}
                        </div>
                      {/if}
                    </div>
                    {#if item.description}
                      <p class="item-description">{item.description}</p>
                    {/if}
                  </div>
                {/each}
              </div>
            {/if}
          </div>
        {/each}
      </div>
    </div>
  </section>

  <!-- Info Section -->
  <section id="info" class="info-section">
    <div class="container">
      <div class="section-title">
        <h2>Visit Us</h2>
      </div>

      <div class="info-container">
        <div class="info-card">
          <div class="card-icon">
            <i class="hours-icon"></i>
          </div>
          <h3>Hours</h3>
          <ul class="hours-list">
            <li><span>Monday - Friday:</span> 6am - 7pm</li>
            <li><span>Saturday:</span> 7am - 7pm</li>
            <li><span>Sunday:</span> 8am - 6pm</li>
          </ul>
        </div>

        <div class="info-card">
          <div class="card-icon">
            <i class="location-icon"></i>
          </div>
          <h3>Location</h3>
          <address>
            123 Coffee Street<br />
            Beanville, CA 94123
          </address>
          <p class="free-parking">Free parking on site!</p>
        </div>

        <div class="info-card">
          <div class="card-icon">
            <i class="contact-icon"></i>
          </div>
          <h3>Contact</h3>
          <p>Phone: (555) 123-4567</p>
          <p>Email: hello@bennysbeanery.com</p>
          <div class="social-icons">
            <a href="https://facebook.com" aria-label="Facebook"
              ><div class="social-icon facebook"></div></a
            >
            <a href="https://instagram.com" aria-label="Instagram"
              ><div class="social-icon instagram"></div></a
            >
            <a href="https://twitter.com" aria-label="Twitter"
              ><div class="social-icon twitter"></div></a
            >
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- About Section -->
  <section id="about" class="about-section">
    <div class="container">
      <div class="section-title">
        <h2>Our Story</h2>
      </div>

      <div class="about-container">
        <div class="about-image">
          <img src={blairImage} alt="Blair, Owner of Benny's Beanery" />
        </div>
        <div class="about-content">
          <h3>Meet Blair</h3>
          <p>
            Founder and head barista of Benny's Beanery, Blair's passion for
            coffee began over a decade ago. What started as a morning ritual
            quickly blossomed into a lifelong dedication to the perfect cup.
          </p>
          <p>
            Benny's Beanery was born from a desire to create a space where
            community and coffee come together. Our beans are ethically sourced,
            our milk is locally produced, and our passion is poured into every
            cup.
          </p>
          <p>
            We believe that great coffee is more than just a beverage—it's an
            experience, a conversation starter, and a moment of joy in your day.
          </p>
        </div>
      </div>
    </div>
  </section>
</main>

<footer>
  <div class="container">
    <div class="footer-content">
      <div class="footer-logo">
        <h3>Benny's Beanery</h3>
      </div>
      <div class="footer-links">
        {#each sections as section}
          <a href="#{section.id}">{section.label}</a>
        {/each}
      </div>
      <div class="footer-copy">
        <p>
          &copy; {new Date().getFullYear()} Benny's Beanery. All rights reserved.
        </p>
      </div>
    </div>
  </div>
</footer>

<style>
  /* Header Styles */
  header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 100;
    background-color: rgba(255, 255, 255, 0.9);
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    backdrop-filter: blur(10px);
  }

  .navbar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem 0;
  }

  .logo a {
    font-size: 1.5rem;
    font-weight: 700;
    color: var(--primary);
  }

  nav ul {
    display: flex;
    list-style: none;
    gap: 2rem;
  }

  nav a {
    font-weight: 500;
    transition: color 0.3s ease;
  }

  nav a:hover {
    color: var(--accent);
  }

  .hamburger-button {
    background: transparent;
    border: none;
    padding: 0;
    margin: 0;
    cursor: pointer;
    display: none;
    color: var(--primary);
  }

  .hamburger {
    display: flex;
    flex-direction: column;
    gap: 5px;
  }

  .hamburger span {
    display: block;
    width: 25px;
    height: 3px;
    background-color: var(--primary);
    transition: all 0.3s ease;
  }

  /* Hero Section */
  .hero {
    height: 100vh;
    background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
      url("/hero.jpg");
    background-size: cover;
    background-position: center;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding: 0;
  }

  .hero-content {
    max-width: 800px;
    padding: 2rem;
    color: white;
  }

  .hero h1 {
    font-size: 4rem;
    margin-bottom: 1rem;
    color: white;
  }

  .hero p {
    font-size: 1.5rem;
    margin-bottom: 2rem;
  }

  .btn {
    display: inline-block;
    background-color: var(--accent);
    color: white;
    padding: 0.8rem 1.5rem;
    border-radius: 4px;
    font-weight: 600;
    transition: background-color 0.3s ease;
  }

  .btn:hover {
    background-color: darken(var(--accent), 10%);
  }

  /* Menu Section */
  .menu-container {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
  }

  .menu-category {
    background-color: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  .category-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 1.5rem;
    background-color: var(--primary-light);
    color: white;
    cursor: pointer;
    width: 100%;
    border: none;
    text-align: left;
  }

  .category-header h3 {
    margin: 0;
    color: white;
  }

  .toggle-icon {
    font-size: 1.5rem;
    font-weight: bold;
  }

  .category-items {
    padding: 1.5rem;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1.5rem;
  }

  .menu-item {
    border-bottom: 1px solid #eee;
    padding-bottom: 1rem;
  }

  .item-header {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    margin-bottom: 0.5rem;
  }

  .item-description {
    color: var(--text-light);
    font-size: 0.9rem;
  }

  /* Info Section */
  .info-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
  }

  .info-card {
    background-color: white;
    padding: 2rem;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    text-align: center;
  }

  .card-icon {
    width: 60px;
    height: 60px;
    margin: 0 auto 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: var(--primary-light);
    border-radius: 50%;
    color: white;
  }

  .hours-list {
    list-style: none;
    text-align: left;
  }

  .hours-list li {
    display: flex;
    justify-content: space-between;
    margin-bottom: 0.5rem;
  }

  .free-parking {
    margin-top: 1rem;
    color: var(--accent);
    font-weight: 600;
  }

  .social-icons {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-top: 1rem;
  }

  .social-icon {
    width: 30px;
    height: 30px;
    background-color: var(--primary);
    border-radius: 50%;
  }

  /* About Section */
  .about-container {
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: 3rem;
    align-items: center;
  }

  .about-image img {
    width: 100%;
    border-radius: 8px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  }

  /* Footer */
  footer {
    background-color: var(--primary-dark);
    color: white;
    padding: 3rem 0;
    margin-top: 2rem;
  }

  .footer-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1.5rem;
  }

  .footer-links {
    display: flex;
    gap: 1.5rem;
  }

  .footer-links a {
    color: var(--primary-light);
    transition: color 0.3s ease;
  }

  .footer-links a:hover {
    color: white;
  }

  .footer-copy {
    margin-top: 1rem;
    color: var(--primary-light);
    font-size: 0.9rem;
  }

  /* Responsive Styles */
  @media (max-width: 768px) {
    .hamburger-button {
      display: block;
      z-index: 101;
    }

    nav {
      position: fixed;
      top: 0;
      right: -100%;
      width: 70%;
      height: 100vh;
      background-color: white;
      flex-direction: column;
      padding: 6rem 2rem;
      transition: right 0.3s ease;
      box-shadow: -5px 0 15px rgba(0, 0, 0, 0.1);
    }

    nav.active {
      right: 0;
    }

    nav ul {
      flex-direction: column;
      align-items: flex-start;
    }

    .about-container {
      grid-template-columns: 1fr;
    }

    .about-image {
      order: 2;
    }

    .about-content {
      order: 1;
    }

    .hero h1 {
      font-size: 3rem;
    }

    .hero p {
      font-size: 1.2rem;
    }
  }
</style>
