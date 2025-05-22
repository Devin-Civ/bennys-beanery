<script lang="ts">
  export let title: string;
  export let iconSrc: string = "";
</script>

<div class="info-card">
  <div class="card-icon">
    <img src={iconSrc} alt={`${title} icon`} class="icon-img" />
  </div>
  <h3>{title}</h3>
  <slot></slot>
</div>

<style>
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

  .icon-img {
    width: 30px;
    height: 30px;
    filter: invert(1); /* Makes the icon white */
  }
</style>
