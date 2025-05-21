<script lang="ts">
  import MenuItem from "./MenuItem.svelte";

  export let category: { name: string; id: string };
  export let items: any[] = [];

  let isExpanded = false;

  function toggleExpand() {
    isExpanded = !isExpanded;
  }
</script>

<div class="menu-category">
  <button
    class="category-header"
    on:click={toggleExpand}
    aria-expanded={isExpanded}
    aria-controls={`category-${category.id}-items`}
  >
    <h3>{category.name}</h3>
    <span class="toggle-icon">
      {isExpanded ? "−" : "+"}
    </span>
  </button>

  {#if isExpanded}
    <div class="category-items" id={`category-${category.id}-items`}>
      {#each items as item}
        <MenuItem {item} />
      {/each}
    </div>
  {/if}
</div>

<style>
  .menu-category {
    background-color: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    margin-bottom: 1.5rem;
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
    color: var(--primary-dark);
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
</style>
