<script lang="ts">
  import InfoCard from "./InfoCard.svelte";
  import clockIcon from "../assets/clock-icon.svg";
  import locationIcon from "../assets/location-icon.svg";
  import contactIcon from "../assets/contact-icon.svg";
  import instagramIcon from "../assets/instagram-icon.svg";
</script>

<section id="info" class="info-section">
  <div class="container">
    <div class="section-title">
      <h2>Visit Us</h2>
    </div>

    <div class="info-container">
      <InfoCard title="Hours" iconSrc={clockIcon}>
        <ul class="hours-list">
          <li><span>Monday:</span> 9am - 3pm</li>
          <li><span>Tuesday:</span> Closed</li>
          <li><span>Wed - Sunday:</span> 9am - 3pm</li>
        </ul>
      </InfoCard>

      <InfoCard title="Location" iconSrc={locationIcon}>
        <address>
          1 Valley Street<br />
          New Haven, CT 06515
        </address>
        <p class="free-parking">Free parking on site!</p>
      </InfoCard>

      <InfoCard title="Contact" iconSrc={contactIcon}>
        <p>
          Phone: <i style="color: grey">Currently Unavailable</i>
        </p>
        <p>Email: blair@bennysbeanery.us</p>
        <div class="social-icons">
          <a
            href="https://instagram.com/bennysbeanery"
            aria-label="Instagram"
            class="social-link"
          >
            <img src={instagramIcon} alt="Instagram" class="social-icon" />
            <span>@bennysbeanery</span>
          </a>
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
    margin-top: 1rem;
  }

  .social-icon {
    width: 24px;
    height: 24px;
    filter: brightness(0) saturate(100%);
    margin-right: 8px;
  }

  .social-link {
    display: flex;
    align-items: center;
    color: var(--primary-dark);
    font-weight: 500;
    transition: color 0.3s ease;
  }

  .social-link:hover {
    color: var(--accent);
  }
</style>
