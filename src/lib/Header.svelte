<script lang="ts">
  // Props
  export let sections: { id: string; label: string }[] = [];
</script>

<header>
  <div class="container">
    <div class="navbar">
      <nav>
        <ul>
          {#each sections as section}
            <li>
              <a href="#{section.id}">{section.label}</a>
            </li>
          {/each}
        </ul>
      </nav>
    </div>
  </div>
</header>
<div class="header-spacer"></div>

<style>
  /* Header Styles */
  header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 100;
    background-color: var(--white);
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    height: var(--header-height);
  }

  .header-spacer {
    height: var(--header-height);
    width: 100%;
  }

  .navbar {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 1rem 0;
    height: 100%;
  }

  nav {
    width: 100%;
  }

  nav ul {
    display: flex;
    list-style: none;
    gap: 3rem;
    justify-content: center;
    align-items: center;
    height: 100%;
  }

  nav a {
    font-family: "Poetsen One", cursive;
    font-weight: 600;
    font-size: 1.4rem;
    transition: color 0.3s ease;
    color: var(--primary-dark);
    padding: 0.5rem 1rem;
  }

  nav a:hover {
    color: var(--accent);
  }
</style>
