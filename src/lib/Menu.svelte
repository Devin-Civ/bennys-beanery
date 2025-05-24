<script lang="ts">
  import { categories } from "./menu.json";

  // Define more specific types
  interface MenuItemBase {
    name: string;
  }

  interface MenuItemWithIngredients extends MenuItemBase {
    ingredients: string[];
  }

  interface MenuItemWithOptions extends MenuItemBase {
    options: string[];
  }

  interface MenuSubcategory extends MenuItemBase {
    isExpandable: boolean;
    items: (
      | MenuItemBase
      | MenuItemWithIngredients
      | MenuItemWithOptions
      | string
    )[];
  }

  // Type guards
  function hasIngredients(item: any): item is MenuItemWithIngredients {
    return item && Array.isArray(item.ingredients);
  }

  function hasOptions(item: any): item is MenuItemWithOptions {
    return item && Array.isArray(item.options);
  }

  function hasItems(item: any): item is MenuSubcategory {
    return item && Array.isArray(item.items);
  }

  // Find the Coffee & Tea category
  const coffeeTeaCategory = categories.find(
    (cat) => cat.name === "Coffee & Tea"
  );

  // Helper function to find menu subcategories
  function findMenuSection(name: string) {
    return coffeeTeaCategory?.items.find((item) => item.name === name);
  }
</script>

<section id="menu" class="menu-section">
  <div class="container">
    <div class="section-title">
      <h2>Our Menu</h2>
    </div>

    <div class="menu-grid">
      <!-- Smoothies Section -->
      {#each categories.filter((cat) => cat.name === "Smoothies") as category}
        <div class="menu-category">
          <h3 class="category-title">{category.name}</h3>

          <div class="menu-items">
            {#each category.items as item}
              <div class="menu-item">
                <div class="item-header">
                  <h4 class="item-name">{item.name}</h4>
                </div>
                {#if hasIngredients(item)}
                  <p class="item-ingredients">
                    {item.ingredients.join(", ")}
                  </p>
                {/if}
              </div>
            {/each}
          </div>

          {#if category.addIns}
            <div class="add-ins">
              <h4 class="option-title">Add-ins</h4>
              <div class="option-items">
                {#each category.addIns as addIn}
                  <span class="option-pill">{addIn}</span>
                {/each}
              </div>
            </div>
          {/if}
        </div>
      {/each}

      <!-- Espresso Drinks Section -->
      {#if coffeeTeaCategory}
        <div class="menu-category">
          <h3 class="category-title">Espresso Drinks</h3>

          <div class="coffee-tea-grid">
            <!-- Specialties -->
            {#if findMenuSection("Specialties")}
              {@const specialties = findMenuSection("Specialties")}
              {#if specialties && hasItems(specialties)}
                <div class="subcategory specialties">
                  <h4 class="subcategory-title">Specialties</h4>
                  <div class="specialty-items">
                    {#each specialties.items as item}
                      {#if typeof item !== "string"}
                        <div class="menu-item specialty">
                          <div class="item-header">
                            <h5 class="item-name">{item.name}</h5>
                          </div>
                          {#if hasIngredients(item)}
                            <p class="item-ingredients">
                              {item.ingredients.join(", ")}
                            </p>
                          {/if}
                        </div>
                      {/if}
                    {/each}
                  </div>
                </div>
              {/if}
            {/if}

            <!-- Espresso -->
            {#if findMenuSection("Espresso")}
              {@const espresso = findMenuSection("Espresso")}
              {#if espresso && hasItems(espresso)}
                <div class="subcategory espresso">
                  <h4 class="subcategory-title">Espresso</h4>
                  <div class="espresso-items">
                    {#each espresso.items as item}
                      {#if typeof item !== "string"}
                        <div class="menu-item">
                          <div class="item-header">
                            <h5 class="item-name">{item.name}</h5>
                          </div>
                          {#if hasIngredients(item)}
                            <p class="item-ingredients">
                              {item.ingredients.join(", ")}
                            </p>
                          {/if}
                        </div>
                      {/if}
                    {/each}
                  </div>
                </div>
              {/if}
            {/if}
          </div>
        </div>

        <!-- Coffee & Tea Section -->
        <div class="menu-category">
          <h3 class="category-title">Coffee & Tea</h3>

          <div class="coffee-tea-grid">
            <!-- Coffee (Cold Brew, Nitro) -->
            <div class="subcategory simple-items">
              <h4 class="subcategory-title">Coffee</h4>
              <div class="simple-items-container">
                {#each coffeeTeaCategory.items.filter((item) => !hasItems(item) && (item.name === "Cold Brew" || item.name === "Nitro")) as item}
                  <div class="menu-item">
                    <div class="item-header">
                      <h5 class="item-name">{item.name}</h5>
                    </div>
                    {#if hasIngredients(item)}
                      <p class="item-ingredients">
                        {item.ingredients.join(", ")}
                      </p>
                    {/if}
                  </div>
                {/each}
              </div>
            </div>

            <!-- Teas -->
            {#if findMenuSection("Teas")}
              {@const teas = findMenuSection("Teas")}
              {#if teas && hasItems(teas)}
                <div class="subcategory teas">
                  <h4 class="subcategory-title">Teas</h4>
                  <div class="tea-items">
                    {#each teas.items as item}
                      {#if typeof item !== "string"}
                        <div class="menu-item">
                          <div class="item-header">
                            <h5 class="item-name">{item.name}</h5>
                          </div>
                          {#if hasOptions(item)}
                            <p class="item-options">
                              Options: {item.options.join(", ")}
                            </p>
                          {/if}
                        </div>
                      {/if}
                    {/each}
                  </div>
                </div>
              {/if}
            {/if}
          </div>

          <!-- Options section (Flavors and Milk) -->
          <div class="options-section">
            <!-- Flavors -->
            {#if findMenuSection("Flavors")}
              {@const flavors = findMenuSection("Flavors")}
              {#if flavors && hasItems(flavors)}
                <div class="option-group">
                  <h4 class="option-title">Flavors</h4>
                  <div class="option-items">
                    {#each flavors.items as flavor}
                      <span class="option-pill"
                        >{typeof flavor === "string"
                          ? flavor
                          : flavor.name}</span
                      >
                    {/each}
                  </div>
                </div>
              {/if}
            {/if}

            <!-- Milk -->
            {#if findMenuSection("Milk")}
              {@const milks = findMenuSection("Milk")}
              {#if milks && hasItems(milks)}
                <div class="option-group">
                  <h4 class="option-title">Milk Options</h4>
                  <div class="option-items">
                    {#each milks.items as milk}
                      <span class="option-pill"
                        >{typeof milk === "string" ? milk : milk.name}</span
                      >
                    {/each}
                  </div>
                </div>
              {/if}
            {/if}
          </div>
        </div>
      {/if}
    </div>
  </div>
</section>

<style>
  .menu-section {
    padding: var(--section-padding);
    background-color: var(--background);
    color: var(--text, #333);
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

  .menu-grid {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4rem;
    max-width: 1000px;
    margin: 0 auto;
  }

  .menu-category {
    padding: 2rem;
    border-radius: 8px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
    background-color: white;
    width: 100%;
  }

  .category-title {
    font-size: 1.8rem;
    margin-bottom: 1.5rem;
    padding-bottom: 0.8rem;
    border-bottom: 2px solid var(--accent, #aa8855);
    color: var(--primary, #553300);
  }

  .menu-items {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1.5rem;
  }

  .menu-item {
    margin-bottom: 1.2rem;
  }

  .item-header {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    margin-bottom: 0.3rem;
  }

  .item-name {
    font-size: 1.2rem;
    margin: 0;
    color: var(--primary, #553300);
  }

  .item-ingredients,
  .item-options {
    font-size: 0.9rem;
    color: var(--text-light, #666);
    margin: 0.3rem 0 0;
    line-height: 1.4;
  }

  .add-ins {
    margin-top: 2rem;
    padding-top: 1rem;
    border-top: 1px dashed #ddd;
  }

  .add-ins h4 {
    margin-bottom: 0.5rem;
    font-size: 1.1rem;
    color: var(--primary, #553300);
  }

  /* Coffee & Tea specific styles */
  .coffee-tea-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 2rem;
    margin-bottom: 2rem;
  }

  .subcategory {
    margin-bottom: 1.5rem;
  }

  .subcategory-title {
    font-size: 1.3rem;
    margin-bottom: 1rem;
    padding-bottom: 0.5rem;
    border-bottom: 1px solid #eee;
    color: var(--primary, #553300);
  }

  .simple-items-container {
    display: flex;
    flex-direction: column;
    gap: 0.8rem;
  }

  .options-section {
    margin-top: 2rem;
    padding-top: 1.5rem;
    border-top: 1px solid #eee;
  }

  .option-group {
    margin-bottom: 1.5rem;
  }

  .option-title {
    margin-bottom: 0.8rem;
    font-size: 1.2rem;
    color: var(--primary, #553300);
  }

  .option-items {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .option-pill {
    display: inline-block;
    padding: 0.3rem 0.8rem;
    background-color: var(--accent-light, #f9f2e8);
    border-radius: 20px;
    font-size: 0.9rem;
    color: var(--primary, #553300);
  }

  /* Responsive adjustments */
  @media (min-width: 768px) {
    .menu-grid {
      flex-direction: row;
      flex-wrap: wrap;
      justify-content: center;
    }

    .menu-category {
      flex: 1 1 400px;
      max-width: 600px;
    }
  }

  @media (max-width: 767px) {
    .coffee-tea-grid {
      grid-template-columns: 1fr;
    }

    .section-title h2 {
      font-size: 2rem;
    }

    .category-title {
      font-size: 1.5rem;
    }

    .menu-category {
      padding: 1.5rem;
      width: 100%;
      max-width: 100%;
    }

    .menu-items {
      grid-template-columns: 1fr;
    }
  }
</style>
