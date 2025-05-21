<script lang="ts">
  import blairImage from "../assets/blair.JPEG";

  export let ownerName = "Blair";
</script>

<section id="about" class="about-section">
  <div class="container">
    <div class="section-title">
      <h2>Our Story</h2>
    </div>

    <div class="about-container">
      <div class="about-image">
        <img src={blairImage} alt="{ownerName}, Owner of Benny's Beanery" />
      </div>
      <div class="about-content">
        <h3>Meet {ownerName}</h3>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque
          vehicula, urna eu facilisis fermentum, justo libero tincidunt arcu,
          nec tincidunt nunc lorem a justo.
        </p>
        <p>
          Curabitur non nulla sit amet nisl tempus convallis quis ac lectus.
          Nulla porttitor accumsan tincidunt. Vivamus suscipit tortor eget felis
          porttitor volutpat.
        </p>
        <p>
          Donec sollicitudin molestie malesuada. Vivamus magna justo, lacinia
          eget consectetur sed, convallis at tellus.
        </p>
      </div>
    </div>
  </div>
</section>

<style>
  .about-section {
    padding: var(--section-padding);
    background-color: var(--background);
  }

  .about-container {
    gap: 3rem;
    align-items: center;
  }

  .about-image img {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    filter: grayscale(20%) brightness(90%);
    border: 3px solid var(--primary-light);
    object-fit: cover;
    margin-bottom: 1rem;
  }

  @media (max-width: 768px) {
    .about-container {
      grid-template-columns: 1fr;
    }

    .about-image {
      order: 2;
    }

    .about-content {
      order: 1;
    }
  }
</style>
