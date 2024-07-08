<script>
    let userGuessInput = '';
    let randomNumber = Math.floor(Math.random() * 100) + 1; 
    let message = '';
    let attempts = 0;
    let lowestAttempts = Infinity; 
    /**
     * @type {HTMLInputElement}
     */
    let inputRef;
  
    function handleGuess() {
      let userGuess = parseInt(userGuessInput);
      attempts++;
  
      if (userGuess === randomNumber) {
        message = "Congratulations! You guessed the correct number.";
        if (attempts < lowestAttempts) {
          lowestAttempts = attempts;
        }
        resetGame();
      } else if (userGuess < randomNumber) {
        message = "Your guess is too low. Guess again!";
      } else {
        message = "Your guess is too high. Guess again!";
      }
  
      userGuessInput = '';
      inputRef.focus();
    }
  
    function resetGame() {
      randomNumber = Math.floor(Math.random() * 100) + 1;
      attempts = 0;
      message += " A new number has been generated. Try to guess it!";
    }

    /**
     * @param {{ key: string; }} event
     */
    function handleKeydown(event) {
    if (event.key === "Enter") {
      handleGuess();
    }
  }
  </script>
  <div class="container">
    <p class="message">{message}</p>

    <input type="number" 
        bind:value={userGuessInput} 
        bind:this={inputRef} 
        title="Enter a number between 1 and 100...Goodluck!" 
        placeholder="Enter Your Guess Here" 
        on:keydown={handleKeydown} 
    />
    <label for="userGuessInput">Enter Guess</label>
    <button on:click={handleGuess}>Submit</button>
  
    {#if attempts > 0}
    <p id="attempts">Attempts this game: {attempts}</p>
    {/if}
  
    {#if lowestAttempts < Infinity}
    <p id="attemptsRecord">Attempts Record: {lowestAttempts}</p>
    {/if}
  </div>
  
  <style>
    .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    text-align: center;
  }
  .message {
    font-size: 5em;
    font-weight: bold;
    margin-bottom: 1rem;
  }

  label {
    display: block;
    margin-bottom: 0.5rem;
  }

  input {
    padding: 5px;
    font-size: 20px;
    margin-bottom: 0.5rem;
  }

  button {
    font-size: 1.4em;
    width: 6em;
    height: 6em;
    border-radius: 50%;
    background: radial-gradient(circle at 25% 25%, hsl(0, 100%, 50%) 0, hsl(0, 100%, 40%) 100%);
    box-shadow: 0 8px 0 hsl(0, 100%, 30%), 2px 12px 10px rgba(0, 0, 0, 0.35);
    color: hsl(0, 100%, 30%);
    text-shadow: -1px -1px 2px rgba(0, 0, 0, 0.3), 1px 1px 2px rgba(255, 255, 255, 0.4);
    text-transform: uppercase;
    letter-spacing: 0.05em;
    transform: translate(0, -8px);
    transition: all 0.2s;
  }

  button:active {
    transform: translate(0, -2px);
    box-shadow: 0 2px 0 hsl(0, 100%, 30%), 2px 6px 10px rgba(0, 0, 0, 0.35);
  }

  p {
    margin: 0.5em 0;
  }
  </style>