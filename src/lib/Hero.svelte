<script lang="ts">
  // Props can be added here if needed
  export let title = "Benny's Beanery";
  export let buttonText = "Order Now";
  export let buttonLink = "#menu";
</script>

<section id="home" class="hero">
  <div class="hero-content">
    <h1>{title}</h1>
    <img src="/src/assets/benny.svg" alt="Benny's Beanery Logo" class="logo" />
    <a href={buttonLink} class="btn">
      <img
        src="/src/assets/doordash.svg"
        alt="DoorDash"
        class="doordash-icon"
      />
      {buttonText}
    </a>
  </div>
</section>

<style>
  /* Hero Section */
  .hero {
    height: 80vh; /* Reduced from 100vh to make it smaller */
    background-image: url("/hero.jpg");
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
    padding-left: 1rem;
    padding-right: 1rem;
    color: var(--primary-dark);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 2rem;
  }

  .logo {
    width: 200px;
    height: auto;
    filter: var(--primary-dark-filter, brightness(0) saturate(100%));
  }

  .hero h1 {
    font-size: 3.5rem;
    margin: 0;
    color: var(--primary-dark);
    font-family: "Poetsen One", cursive;
  }

  .btn {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    background-color: var(--accent);
    color: var(--primary-dark);
    padding: 0.8rem 1.5rem;
    border-radius: 20px;
    font-weight: 600;
    transition: background-color 0.3s ease;
  }

  .doordash-icon {
    width: 24px;
    height: 24px;
    filter: brightness(0) saturate(100%);
  }

  .btn:hover {
    outline: 3px solid var(--primary-dark);
  }

  /* Responsive Styles */
  @media (max-width: 768px) {
    .hero {
      height: 70vh; /* Smaller on mobile */
    }

    .hero-content {
      gap: 1.5rem;
    }

    .logo {
      width: 150px;
    }

    .hero h1 {
      font-size: 2.5rem;
      max-width: 300px;
    }
  }
</style>
