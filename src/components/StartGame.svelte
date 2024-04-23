<script>
  // input user and click start
  // then the user can the game cleary
  // if (isStartClicked) hide the component and show the game
</script>

<main class="start-form-container">
  <form>
    <div class="start-container">
      <div class="start-name-container">
        <label for="name">Name</label>
        <input id="name" />
      </div>
      <button>Start</button>
    </div>
  </form>
</main>

<style>
  .start-form-container {
    position: absolute;
    width: 28rem;
    height: 30rem;
    margin-top: 13.5rem;
    margin-left: 8.5rem;
    background-color: rgb(28, 135, 134);
    opacity: 0.95;
    z-index: 1;
    border-radius: 10px;
  }

  .start-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 20px;
    margin: 20px;
    font-size: 2rem;
    height: 25rem;
  }

  .start-name-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-bottom: 50px;
    gap: 20px;
  }

  input {
    width: 12rem;
    height: 2rem;
    border-radius: 5px;
  }

  button {
    font-size: 1.5rem;
    width: 10rem;
    height: 5rem;
    border-radius: 5px;
    background-color: rgb(255, 235, 58);
    cursor: pointer;
  }
</style>
