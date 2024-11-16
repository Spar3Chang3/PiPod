<script lang="js">
  let highlightSelection = {
    spotify: "spotify-icon",
    local: "files-icon"
  }

  let buttons = [];
  let currentButton = 0;

  const focusButton = () => {
    buttons[currentButton]?.focus();
  };

  const handleKeyDown = (e) => {
    if (e.key === 'ArrowDown') {
      currentButton = (currentButton + 1) % buttons.length;
    } else if (e.key === 'ArrowUp') {
      currentButton = (currentButton - 1 + buttons.length) % buttons.length;
    }

    focusButton();
  }

  let currentSelection = highlightSelection.spotify;
</script>
<main>

  <section class="status-bar">

  </section>

  <section class="welcome-message">
    <h1>Welcome, Daryk</h1>
  </section>

  <section class="selection-box" aria-label="Selection Buttons" role="region" tabindex="0" aria-selected="true" on:keydown={handleKeyDown}>
    <div class="spotify-portal portal">
      <button bind:this={buttons[0]} autofocus on:focus={() => currentSelection = highlightSelection.spotify}>
        Spotify
      </button>
      <span style="opacity: {currentSelection === highlightSelection.spotify ? '1' : '0'}">
        >
      </span>
    </div>

    <div class="local-portal portal">
      <button bind:this={buttons[1]} on:focus={() => currentSelection = highlightSelection.local}>
        Local
      </button>
      <span style="opacity: {currentSelection === highlightSelection.spotify ? '0' : '1'}">
        >
      </span>
    </div>
  </section>

  <section class="icon-container">
    <img src="./assets/${currentSelection}.svg" alt="Selected feature icon" class="icon-display"/>
  </section>
</main>
<style>
  .welcome-message {
    width: 100vw;
    text-align: center;
  }

  .selection-box {
    display: flex;
    flex-direction: column;
    width: 100vw;
  }

  .portal {
    position: relative;
    display: inline-flex;
    align-items: center;
    height: 10%;
    width: 100%;
    border-top: 0.1rem solid white;
    border-bottom: 0.1rem solid white;
    margin-bottom: 2.5%;

    button {
      height: 100%;
      width: 100%;
      background-color: rgba(36, 36, 36, 1);
      border: none;
      font-size: xx-large;
      justify-content: space-between;
    }

    button:focus {
      background-color: #B9D5BC;
      outline: none;
    }

    span {
      position: absolute;
      width: 90%;
      background: none;
      text-align: right;
      font-size: xxx-large;
    }
  }

  .icon-container {
    display: flex;
    height: 25vh;
    width: 100vw;
    justify-content: center;
    align-items: center;
  }

  .icon-display {
    height: 90%;
    width: 90%;
    image-rendering: optimizeQuality;
    transition: fade 500ms;
  }
</style>