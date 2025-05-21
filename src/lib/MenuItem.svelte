<script lang="ts">
  export let item: any;
</script>

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

<style>
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
</style>
