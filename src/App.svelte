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
    {#each items as item}
      <li class="item">
        <div class="card">
          <button tabindex="0">
            <img src={item.src} alt="placeholder" />
          </button>
        </div>
      </li>
    {/each}
  </ul>

  <h2>Use tab or hover to trigger the effect</h2>
</main>

<style>
  .items {
    width: 100%;
    display: flex;
    gap: 1rem;
  }

  .item {
    perspective: 1000px;
    position: relative;
    z-index: 0;
  }

  .item:hover,
  .items:not(:has(:hover)) .item:focus-within {
    z-index: 1;
  }

  .card {
    filter: brightness(0);
    transform-style: preserve-3d;
    transition: 0.15s;
  }

  .card img {
    width: 100px;
    display: block;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  }

  .item:hover .card,
  .items:not(:has(:hover)) .item:focus-within .card {
    filter: brightness(1);
    transform: translateZ(250px);
  }

  .item:hover + .item .card,
  .items:not(:has(:hover)) .item:focus-within + .item .card {
    filter: brightness(0.5);
    transform: translateZ(150px) rotateY(40deg);
  }

  .item:hover + .item + .item .card,
  .items:not(:has(:hover)) .item:focus-within + .item + .item .card {
    filter: brightness(0.25);
    transform: translateZ(100px) rotateY(20deg);
  }

  .item:hover + .item + .item + .item .card,
  .items:not(:has(:hover)) .item:focus-within + .item + .item + .item .card {
    filter: brightness(0.1);
    transform: translateZ(10px);
  }

  .item:has(+ .item:hover) .card,
  .items:not(:has(:hover)) .item:has(+ .item:focus-within) .card {
    filter: brightness(0.5);
    transform: translateZ(150px) rotateY(-40deg);
  }

  .item:has(+ .item + .item:hover) .card,
  .items:not(:has(:hover)) .item:has(+ .item + .item:focus-within) .card {
    filter: brightness(0.25);
    transform: translateZ(100px) rotateY(-20deg);
  }

  .item:has(+ .item + .item + .item:hover) .card,
  .items:not(:has(:hover))
    .item:has(+ .item + .item + .item:focus-within)
    .card {
    filter: brightness(0.1);
    transform: translateZ(10px);
  }
</style>
