<script lang="ts">
  import blairImage from "../assets/blair.JPEG";
</script>

<section id="about" class="about-section">
  <div class="container">
    <div class="section-title">
      <h2>About Us</h2>
    </div>

    <div class="about-container">
      <div class="about-image">
        <img src={blairImage} alt="Blair, Owner of Benny's Beanery" />
      </div>
      <div class="about-content">
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
      </div>
    </div>
  </div>
</section>

<style>
  .about-section {
    padding: var(--section-padding);
    background-color: var(--background);
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 1rem;
  }

  .section-title {
    text-align: center;
    margin-bottom: 3rem;
  }

  .section-title h2 {
    font-size: 2.5rem;
    position: relative;
    display: inline-block;
  }

  .section-title h2:after {
    content: "";
    display: block;
    width: 50%;
    height: 3px;
    background-color: var(--accent, #aa8855);
    margin: 0.5rem auto 0;
  }

  .about-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 3rem;
    max-width: 1000px;
    margin: 0 auto;
  }

  .about-image img {
    width: 300px;
    height: 300px;
    border-radius: 8px;
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
    object-fit: cover;
    transition: transform 0.3s ease;
  }

  .about-image img:hover {
    transform: scale(1.02);
  }

  .about-content {
    text-align: center;
    line-height: 1.6;
  }

  .about-content p {
    margin-bottom: 1.5rem;
  }

  @media (min-width: 768px) {
    .about-container {
      flex-direction: row;
      text-align: left;
      justify-content: center;
    }

    .about-content {
      text-align: left;
      max-width: 600px;
    }
  }

  @media (max-width: 767px) {
    .about-container {
      flex-direction: column;
    }

    .about-image {
      order: 1;
      margin-bottom: 1.5rem;
    }

    .about-content {
      order: 2;
    }

    .section-title h2 {
      font-size: 2rem;
    }

    .about-image img {
      width: 250px;
      height: 250px;
    }
  }
</style>
