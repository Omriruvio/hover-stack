<script lang="ts">
  const items = Array.from({ length: 15 }, (_, i) => ({
    src: `https://placehold.co/250x400`,
    id: i,
  }));

  document.addEventListener("keydown", (e) => {
    if (e.key === "Escape") {
      (document.activeElement as HTMLElement)?.blur();
    }
  });
</script>

<main>
  <ul class="items">
    {#each items as item (item)}
      <li class="item">
        <button tabindex="0">
          <img src={item.src} alt="placeholder" />
        </button>
      </li>
    {/each}
  </ul>

  <h2>Use tab or hover to trigger the effect</h2>
</main>

<style>
  h2 {
    text-align: center;
    margin-top: 5rem;
  }

  ul {
    list-style-type: none;
    padding: 0;
    display: flex;
    align-items: center;

    & li {
      padding: 0.2rem;
    }
  }

  .items {
    width: 100%;
    display: flex;
    justify-content: center;
    flex-direction: row;

    perspective: 1000px;
    transform-style: preserve-3d;
  }

  .item {
    filter: brightness(0);
    transition: 0.15s;

    & img {
      width: 100px;
      display: block;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
    }
  }

  .item:hover,
  .items:not(:has(:hover)) .item:focus-within {
    filter: brightness(1);
    transform: translateZ(200px);
  }

  .item:hover + *,
  .items:not(:has(:hover)) .item:focus-within + * {
    filter: brightness(0.5);
    transform: translateZ(150px) rotateY(40deg);
  }

  .item:hover + * + *,
  .items:not(:has(:hover)) .item:focus-within + * + * {
    filter: brightness(0.25);
    transform: translateZ(100px) rotateY(20deg);
  }

  .item:hover + * + * + *,
  .items:not(:has(:hover)) .item:focus-within + * + * + * {
    filter: brightness(0.1);
    transform: translateZ(10px);
  }

  .item:has(+ *:hover),
  .items:not(:has(:hover)) .item:has(+ *:focus-within) {
    filter: brightness(0.5);
    transform: translateZ(150px) rotateY(-40deg);
  }

  .item:has(+ * + *:hover),
  .items:not(:has(:hover)) .item:has(+ * + *:focus-within) {
    filter: brightness(0.25);
    transform: translateZ(100px) rotateY(-20deg);
  }

  .item:has(+ * + * + *:hover),
  .items:not(:has(:hover)) .item:has(+ * + * + *:focus-within) {
    filter: brightness(0.1);
    transform: translateZ(10px);
  }
</style>
