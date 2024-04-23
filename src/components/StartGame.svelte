<script>
  import { getDatabase, ref, push } from "firebase/database";
  let username;
  let isStartClicked = false;

  const formSubmitHandler = () => {
    if (username.length < 2) {
      alert("Your name is too short");
    } else {
      const db = getDatabase();
      push(ref(db, "users/"), {
        username,
        correct_count: 0,
      });

      isStartClicked = true;
    }
  };
</script>

{#if !isStartClicked}
  <main class="start-form-container">
    <form on:submit|preventDefault={formSubmitHandler}>
      <div class="start-container">
        <div class="start-name-container">
          <label for="name">Name</label>
          <input id="name" bind:value={username} />
        </div>
        <button type="submit">Start</button>
      </div>
    </form>
  </main>
{/if}

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
