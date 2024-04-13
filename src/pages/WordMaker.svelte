<script>
  import Header from "../components/Header.svelte";
</script>

<Header />

<main>
  <div class="maker-description">
    Make your own word search game on any topic you like, simply by providing
    between 10 and 20 words. Once submitted, your puzzle will be instantly
    playable on-line as well as easily printed, so you can share it with
    friends. Instructions are available at the bottom of this page
  </div>
  <div class="maker-form_container">
    <form class="maker-form">
      <div class="title-container">
        <label for="title">Title</label>
        <input class="title" type="text" required />
      </div>
      <div class="description-container">
        <label for="description">Description</label>
        <input class="description" type="text" required />
      </div>
      <div class="word-list-container">
        <label for="word-list">Word List</label>
        <p>
          Between 10 and 20 words. Puzzles are randomly generated using a
          selection of your words at play time.
        </p>
        <div class="word-list">
          <div class="word-list-row1">
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
          </div>
          <div class="word-list-row2">
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
          </div>
          <div class="word-list-row3">
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
          </div>
          <div class="word-list-row4">
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
            <input class="word" type="text" required />
          </div>
        </div>
      </div>
    </form>
  </div>
</main>

<style>
  main {
    padding: 20px 15px 20px 15px;
    margin: 0 100px 0 100px;
  }
  .maker-description {
    display: flex;
    justify-content: center;
    text-align: center;
    margin-bottom: 20px;
    font-size: 17px;
  }

  .maker-form {
    font-size: 1.3rem;
  }

  .title-container,
  .description-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin-bottom: 10px;
  }

  .title {
    height: 30px;
  }

  .description {
    height: 50px;
  }

  p {
    margin: 0 0 10px 0;
  }

  .word-list {
    width: 1200px;
  }

  .word {
    width: 225px;
    height: 30px;
    font-size: 1rem;
  }
</style>
