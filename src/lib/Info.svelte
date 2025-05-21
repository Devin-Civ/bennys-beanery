<script lang="ts">
  import InfoCard from "./InfoCard.svelte";
</script>

<section id="info" class="info-section">
  <div class="container">
    <div class="section-title">
      <h2>Visit Us</h2>
    </div>

    <div class="info-container">
      <InfoCard title="Hours" iconClass="hours-icon">
        <ul class="hours-list">
          <li><span>Monday - Friday:</span> 6am - 7pm</li>
          <li><span>Saturday:</span> 7am - 7pm</li>
          <li><span>Sunday:</span> 8am - 6pm</li>
        </ul>
      </InfoCard>

      <InfoCard title="Location" iconClass="location-icon">
        <address>
          123 Coffee Street<br />
          Beanville, CA 94123
        </address>
        <p class="free-parking">Free parking on site!</p>
      </InfoCard>

      <InfoCard title="Contact" iconClass="contact-icon">
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
      </InfoCard>
    </div>
  </div>
</section>

<style>
  .info-section {
    padding: var(--section-padding);
    background-color: var(--white);
  }

  .info-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
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
</style>
