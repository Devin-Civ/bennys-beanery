<script lang="ts">
  import MenuCategory from "./MenuCategory.svelte";
  import menuData from "./menu.json";

  // Menu categories based on the requirements
  export let menuCategories = [
    { name: "Specialty Drinks", id: "specialties" },
    { name: "Smoothies", id: "smoothies" },
    { name: "Coffee", id: "coffee" },
    { name: "Matcha/Tea", id: "tea" },
  ];

  // Find menu items for each category
  function getCategoryItems(categoryName: string): any[] {
    if (categoryName === "Specialty Drinks") {
      return (
        (menuData.categories.find((c) => c.name === "Specialties")
          ?.items as any[]) || []
      );
    } else if (categoryName === "Smoothies") {
      return (
        (menuData.categories.find((c) => c.name === "Smoothies")
          ?.items as any[]) || []
      );
    } else if (categoryName === "Coffee") {
      const coffeeItems = menuData.categories
        .filter((c) => ["Espresso", "Cold Brew & Nitro"].includes(c.name))
        .flatMap((c) => c.items as any[]);
      return coffeeItems || [];
    } else if (categoryName === "Matcha/Tea") {
      return (
        (menuData.categories.find((c) => c.name === "Teas")?.items as any[]) ||
        []
      );
    }
    return [];
  }
</script>

<section id="menu" class="menu-section">
  <div class="container">
    <div class="section-title">
      <h2>Our Menu</h2>
    </div>

    <div class="menu-container">
      {#each menuCategories as category}
        <MenuCategory {category} items={getCategoryItems(category.name)} />
      {/each}
    </div>
  </div>
</section>

<style>
  .menu-section {
    padding: var(--section-padding);
    background-color: var(--background);
  }

  .menu-container {
    margin-top: 2rem;
  }
</style>
