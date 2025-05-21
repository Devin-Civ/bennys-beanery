<footer>
  <div class="container">
    <div class="footer-content">
      <div class="footer-copy">
        <p>
          &copy; {new Date().getFullYear()} Benny's Beanery. All rights reserved.
        </p>
      </div>
    </div>
  </div>
</footer>

<style>
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

  .footer-copy {
    margin-top: 1rem;
    color: var(--primary-light);
    font-size: 0.9rem;
  }
</style>
