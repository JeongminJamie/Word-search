<script>
  import Header from "../components/Header.svelte";

  import { getDatabase, ref, push } from "firebase/database";

  const db = getDatabase();

  let title;
  let description;
  let word1;
  let word2;
  let word3;
  let word4;
  let word5;
  let word6;
  let word7;
  let word8;
  let word9;
  let word10;
  let word11;
  let word12;
  let word13;
  let word14;
  let word15;
  let word16;
  let word17;
  let word18;
  let word19;
  let word20;

  let wordList = [];
  let isSubmitted = false;
  let gameUrl;

  const addtoWordList = (word) => {
    if (word.length > 2 && word.length < 7) {
      wordList.push(word);
    } else {
      alert("Word is too short or long");
    }
  };

  const handleSubmit = () => {
    try {
      if (wordList.length >= 10 && wordList.length <= 20) {
        push(ref(db, "games/"), {
          title,
          description,
          words: wordList,
        });
        isSubmitted = true;
        gameUrl = `http://localhost:5173/#/puzzles/${title}`
      } else alert("Please fill out more than 10 fields");
    } catch (e) {
      console.log(e);
    }
  };
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
    <form class="maker-form" on:submit|preventDefault={handleSubmit}>
      <div class="title-container">
        <label for="title">Title</label>
        <input class="title" type="text" bind:value={title} required />
      </div>
      <div class="description-container">
        <label for="description">Description</label>
        <input
          class="description"
          type="text"
          bind:value={description}
          required
        />
      </div>
      <div class="word-list-container">
        <label for="word-list">Word List</label>
        <p>
          Between 10 and 20 words. Every word should consist of between 3 to 6
          letters. Puzzles are randomly generated using a selection of your
          words at play time.
        </p>
        <div class="word-list">
          <div class="word-list-row1">
            <input
              class="word"
              type="text"
              bind:value={word1}
              on:change={() => addtoWordList(word1)}
            />
            <input
              class="word"
              type="text"
              bind:value={word2}
              on:change={() => addtoWordList(word2)}
            />
            <input
              class="word"
              type="text"
              bind:value={word3}
              on:change={() => addtoWordList(word3)}
            />
            <input
              class="word"
              type="text"
              bind:value={word4}
              on:change={() => addtoWordList(word4)}
            />
            <input
              class="word"
              type="text"
              bind:value={word5}
              on:change={() => addtoWordList(word5)}
            />
          </div>
          <div class="word-list-row2">
            <input
              class="word"
              type="text"
              bind:value={word6}
              on:change={() => addtoWordList(word6)}
            />
            <input
              class="word"
              type="text"
              bind:value={word7}
              on:change={() => addtoWordList(word7)}
            />
            <input
              class="word"
              type="text"
              bind:value={word8}
              on:change={() => addtoWordList(word8)}
            />
            <input
              class="word"
              type="text"
              bind:value={word9}
              on:change={() => addtoWordList(word9)}
            />
            <input
              class="word"
              type="text"
              bind:value={word10}
              on:change={() => addtoWordList(word10)}
            />
          </div>
          <div class="word-list-row3">
            <input
              class="word"
              type="text"
              bind:value={word11}
              on:change={() => addtoWordList(word11)}
            />
            <input
              class="word"
              type="text"
              bind:value={word12}
              on:change={() => addtoWordList(word12)}
            />
            <input
              class="word"
              type="text"
              bind:value={word13}
              on:change={() => addtoWordList(word13)}
            />
            <input
              class="word"
              type="text"
              bind:value={word14}
              on:change={() => addtoWordList(word14)}
            />
            <input
              class="word"
              type="text"
              bind:value={word15}
              on:change={() => addtoWordList(word15)}
            />
          </div>
          <div class="word-list-row4">
            <input
              class="word"
              type="text"
              bind:value={word16}
              on:change={() => addtoWordList(word16)}
            />
            <input
              class="word"
              type="text"
              bind:value={word17}
              on:change={() => addtoWordList(word17)}
            />
            <input
              class="word"
              type="text"
              bind:value={word18}
              on:change={() => addtoWordList(word18)}
            />
            <input
              class="word"
              type="text"
              bind:value={word19}
              on:change={() => addtoWordList(word19)}
            />
            <input
              class="word"
              type="text"
              bind:value={word20}
              on:change={() => addtoWordList(word20)}
            />
          </div>
        </div>
      </div>
      <button type="submit">Submit</button>
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
    font-size: 1rem;
    height: 30px;
  }

  .description {
    font-size: 1rem;
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

  button {
    width: 1185px;
    height: 50px;
    font-size: 1.25rem;
    margin-top: 20px;
  }
</style>
