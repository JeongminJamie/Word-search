<script>
  import {
    getDatabase,
    ref,
    query,
    orderByChild,
    equalTo,
    get,
  } from "firebase/database";
  import { onMount } from "svelte";

  import Header from "../components/Header.svelte";
  import StartGame from "../components/StartGame.svelte";

  export let params = {};
  // get the title from the params
  const { title } = params;

  let dataByTitle = [];
  let objectDataFromData;
  // the word list of the title from db --> get from the db
  let wordList = null;

  // function getting the data seeing params.title matches to the title from games table
  const fetchDataByTitle = async (title) => {
    const database = getDatabase();
    const databaseRef = ref(database, "games");
    const dataQuery = query(databaseRef, orderByChild("title"), equalTo(title));
    const snapshot = await get(dataQuery);

    if (snapshot.exists()) {
      return snapshot.val();
    } else {
      console.log("No data available for the title");
      return null;
    }
  };

  //fetching data from the table
  onMount(async () => {
    try {
      dataByTitle = await fetchDataByTitle(title);
      objectDataFromData = Object.values(dataByTitle);
      wordList = objectDataFromData[0].words;
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  });

  // create a grid of upper case alphabets
  // 겉부분의 배열이 rows, 안 부분의 배열이 cols다
  let puzzleGrid = [];
  const rows = 12;
  const cols = 14;

  for (let r = 0; r < rows; r++) {
    let row = [];
    // create 14 columns for each row
    for (let c = 0; c < cols; c++) {
      // generate random characters
      row.push(String.fromCharCode(65 + Math.floor(Math.random() * 26)));
    }
    // add the 12 rows to the puzzleGrid
    puzzleGrid.push(row);
  }

  // put words from the wordList in the puzzleGrid
  $: {
    if (wordList === null) {
      console.log("fetching data...");
    } else {
      wordList.forEach((word) => {
        //decide the direction with 50% of chance using Math.random() < 0.5 ?
        let direction = Math.random() < 0.5 ? "horizontal" : "vertical";
        // make a number for starting position of a row
        let startingRowPosition = Math.floor(
          Math.random() * (rows - word.length),
        );
        //create the starting position in a column
        let startingColumnPosition = Math.floor(
          Math.random() * (cols - word.length),
        );

        if (direction === "horizontal") {
          for (let i = 0; i < word.length; i++) {
            puzzleGrid[startingRowPosition][startingColumnPosition + i] =
              word[i].toUpperCase();
          }
        } else if (direction === "vertical") {
          for (let i = 0; i < word.length; i++) {
            puzzleGrid[startingRowPosition + i][startingColumnPosition] =
              word[i].toUpperCase();
          }
        }
      });
    }
  }

  let selectedWord = "";
  let isMouseDown = false;
  let correctionCount = 0;

  const handleMouseDown = (rowIndex, colIndex) => {
    isMouseDown = true;
    selectedWord += puzzleGrid[rowIndex][colIndex];
  };

  const handleMouseMove = (rowIndex, colIndex) => {
    if (isMouseDown) {
      selectedWord += puzzleGrid[rowIndex][colIndex];
    }
  };

  function handleMouseUp() {
    isMouseDown = false;
    if (wordList !== null && selectedWord.length > 2) {
      if (wordList.includes(selectedWord)) {
        console.log("Correct");
        correctionCount += 1;
      } else {
        console.log("You can do better");
      }
      selectedWord = "";
    }
  }
</script>

<Header />
<StartGame />
<main>
  <div class="game-title">{params.title}</div>
  <div class="game-container">
    <div class="puzzle-grid-container">
      {#each puzzleGrid as row, rowIndex}
        <div class="puzzle-grid-row_cell" role="button" tabindex="0">
          {#each row as randomAlphabet, colIndex}
            <div
              class="puzzle-grid-column_cell"
              role="button"
              tabindex="0"
              on:mousedown={() => handleMouseDown(rowIndex, colIndex)}
              on:mousemove={() => handleMouseMove(rowIndex, colIndex)}
              on:mouseup={handleMouseUp}
            >
              {randomAlphabet}
            </div>
          {/each}
        </div>
      {/each}
    </div>
    <div class="answer-words-list_container">
      {#if wordList !== null}
        {#each wordList as word}
          <div class="answer-word">{word.toUpperCase()}</div>
        {/each}
      {/if}
    </div>
    <div class="time-correction_container">
      <div>Time taken:</div>
      <div class="correction-count">Correction Count: {correctionCount}</div>
    </div>
  </div>
</main>

<style>
  main {
    margin: 40px 50px 20px 50px;
  }
  .game-title {
    font-size: 30px;
    text-transform: capitalize;
  }
  .game-container {
    display: flex;
  }
  .puzzle-grid-container {
    display: flex;
    flex-direction: row;
    align-items: center;
    margin-top: 20px;
    position: relative;
    width: 50%;
  }
  .puzzle-grid-column_cell {
    width: 50px;
    height: 50px;
    border: 1px solid #ccc;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 23px;
  }

  .answer-words-list_container {
    margin: 35px 0px 0px 20px;
    font-size: 20px;
  }

  .answer-word {
    margin-top: 12px;
  }

  .time-correction_container {
    margin-top: 47px;
    margin-left: 50px;
    font-size: 1.5rem;
    font-weight: 550;
  }

  .correction-count {
    margin-top: 10px;
  }
</style>
