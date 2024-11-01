<script>
    import BeamAvatar from './../lib/components/BeamAvatar.svelte';
    import colors from './../lib/data/colors.json';
  
    let currentColors = $state(colors[0]);
  
  let scientists = $state([
    { name: "Marie Curie" },
    { name: "Albert Einstein" },
    { name: "Rosalind Franklin" },
    { name: "Charles Darwin" },
    { name: "Dorothy Hodgkin" },
    { name: "Isaac Newton" },
    { name: "Barbara McClintock" },
    { name: "Stephen Hawking" },
    { name: "Emmy Noether" },
    { name: "Richard Feynman" },
    { name: "Jane Goodall" },
    { name: "Niels Bohr" },
    { name: "Lise Meitner" },
    { name: "Max Planck" },
    { name: "Rachel Carson" },
    { name: "Alan Turing" },
    { name: "Chien-Shiung Wu" },
    { name: "Werner Heisenberg" },
    { name: "Grace Hopper" },
    { name: "Erwin Schrödinger" }
  ]);

  function randomizeColors() {
    const randomIndex = Math.floor(Math.random() * colors.length);
    currentColors = colors[randomIndex];
  }
</script>

<div class="scientist-grid">
  <h1>Beam Boring Avatars - Svelte</h1>
  <button class="randomize-btn" onclick={randomizeColors}>
    Randomize Colors
  </button>
  
  <div class="scientists">
    {#each scientists as scientist, index}
      <div class="scientist-card">
        <div class="avatar-container">
          <BeamAvatar
            name={scientist.name}
            colors={currentColors}
            size={80}
          />
        </div>
        <div class="scientist-info">
          <input
            type="text"
            bind:value={scientist.name}
            class="name-input"
          />
        </div>
      </div>
    {/each}
  </div>

  <footer class="attribution">
    <p>
      Original Boring avatars by 
      <a href="https://github.com/boringdesigners/boring-avatars">Hayk An, Javi Sánchez-Marín, Enric Pallerols and Josep Martins</a>.
    </p>
    <p>
      The color palette samples are from the 
      <a href="https://github.com/Jam3/nice-color-palettes">Nice Color Palettes</a> 
      made by 
      <a href="https://www.mattdesl.com/">Matt DesLauriers</a>.
    </p>
  </footer>
</div>

<style>
  .scientist-grid {
    padding: 32px;
    max-width: 1200px;
    margin: 0 auto;
  }

  h1 {
    text-align: center;
    color: #191815;
    margin-bottom: 32px;
    font-family: 'Poppins', sans-serif;
    font-size: 32px;
  }

  .randomize-btn {
    display: block;
    margin: 0 auto 32px;
    background: #1855F4;
    color: #FFFFFF;
    border: none;
    padding: 12px 24px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
    font-family: 'Poppins', sans-serif;
    transition: opacity 0.2s ease;
  }

  .randomize-btn:hover {
    opacity: 0.9;
  }

  .scientists {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 32px;
    margin-bottom: 48px;
  }

  .scientist-card {
    padding: 24px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 16px;
    transition: transform 0.2s ease;
  }

  .scientist-card:hover {
    transform: translateY(-2px);
  }

  .avatar-container {
    width: 80px;
    height: 80px;
  }

  .scientist-info {
    width: 100%;
  }

  .name-input {
    width: 100%;
    padding: 8px;
    border: 1px solid #E7E0CB;
    border-radius: 6px;
    background: #FFFFFF;
    color: #191815;
    text-align: center;
    font-size: 14px;
    font-family: 'Poppins', sans-serif;
  }

  .name-input:focus {
    outline: none;
    border-color: #1855F4;
  }

  .attribution {
    text-align: center;
    margin-top: 48px;
    padding-top: 24px;
    border-top: 1px solid #E7E0CB;
    font-family: 'Poppins', sans-serif;
    font-size: 14px;
    color: #666666;
    line-height: 1.5;
  }

  .attribution a {
    color: #1855F4;
    text-decoration: none;
  }

  .attribution a:hover {
    text-decoration: underline;
  }

  @media (max-width: 480px) {
    .scientist-grid {
      padding: 16px;
    }

    .name-input {
      font-size: 12px;
      padding: 6px;
    }

    .randomize-btn {
      font-size: 14px;
      padding: 10px 20px;
    }

    .attribution {
      font-size: 12px;
    }
  }
</style>