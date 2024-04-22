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

  export let params = {};
  // get the title from the params
  const { title } = params;
  let dataByTitle = [];
  let objectDataFromData;

  // the word list of the title from db --> get from the db
  let wordList;

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
  $: wordList
    ? wordList.forEach((word) => {
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
              word[i];
          }
        } else if (direction === "vertical") {
          for (let i = 0; i < word.length; i++) {
            puzzleGrid[startingRowPosition + i][startingColumnPosition] =
              word[i];
          }
        }
      })
    : console.log("A Word list doesn't exist");

  let selectedWord = "";

  const selectWord = (row, col) => {
    selectedWord += puzzleGrid[row][col];
  };

  const checkWord = () => {
    if (wordList.includes(selectedWord)) {
      alert("Correct!");
    } else {
      alert("You can do better");
    }
    selectedWord = "";
  };
</script>

<Header />
<!-- 
<div class="puzzle-grid-container">
  {#each puzzleGrid as row, rowIndex}
    <div
      class="puzzle-grid-row_cell"
      role="button"
      tabindex="0"
      on:mousedown={checkWord}
    >
      {#each row as randomAlphabet, colIndex }
        <div class="puzzle-grid-column_cell">{randomAlphabet}</div>
      {/each}
    </div>
  {/each}
</div> -->
<div>{params.title} 게임 페이지입니당</div>
<p>{wordList}</p>