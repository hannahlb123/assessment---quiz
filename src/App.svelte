<script>
  //create empty variables to set up page
	let choice = ''
	let result = ''
  let points = 0
  let name = ''
  let formRoom = ''
  let gameLength = 3
  let started = false
	let library = []
  let questions = []
  let valid = false
	let error = ''
	let i = 0
	let question = questions.at[i]
  let answering = true
  let complete = false
	let age = ''
	
  //start function. when the start button is clicked, generate the library of questions 
  function start() {
		console.log('function start')
		//create a library with a list of question options
    library = [
				{
				 	question:'Does current split or stay constant through a series 			circuit?',
          type: 'multi',
				  option1:'same',
					option2:'splits',
          option3: '',
					answer:'same',
					result:'',
					graphic:'',
					choice:''
				},
				{
					question:'Does voltage stay constant or split in a series circuit?',
          type: 'multi',
					option1:'same',
					option2:'splits',
          option3: '',
					answer:'splits',
					result:'',
					graphic:'',
					choice:''
				},
        {
					question:'What is the voltage across the lightbulb in this circuit?',
          type: 'number',
					answer:'4',
          unit: 'Volts',
					result:'',
					graphic:'../src/assets/images/circuit1.png',
					choice:''
				},
        {
					question:'Does voltage stay constant or split in a parallel circuit?',
          type: 'multi',
					option1:'same',
					option2:'splits',
          option3: '',
					answer:'same',
					result:'',
					graphic:'',
					choice:''
				},
        {
					question:'Does current stay constant or split in a parallel circuit?',
          type: 'multi',
					option1:'same',
					option2:'splits',
					answer:'splits',
          option3: '',
					result:'',
					graphic:'',
					choice:''
				},
        {
					question:'An electric field is set up between parallel plates. A proton is placed between the plates, will it travel with or against the field lines?',
          type: 'multi',
					option1:'with',
					option2:'against',
          option3: '',
					answer:'with',
					result:'',
					graphic:'',
					choice:''
				},
        {
					question:'An electric field is set up between parallel plates. An electron is placed between the plates, will it travel with or against the field lines?',
          type: 'multi',
					option1:'with',
					option2:'against',
          option3: '',
					answer:'against',
					result:'',
					graphic:'',
					choice:''
				},
        {
					question:'The voltmeter reads 4.0V. What is the current around the circuit? Hint: V = IR',
          type: 'number',
					answer:'0.8',
          unit: 'Amps',
					result:'',
					graphic:'../src/assets/images/circuit2.png',
					choice:''
				},
        {
					question:'What does this circuit symbol represent?',
          type: 'multi',
					option1:'switch',
					option2:'lightbulb',
          option3:'voltmeter',
					answer:'lightbulb',
					result:'',
					graphic:'../src/assets/images/lightbulb.png',
					choice:''
				},
        {
					question:'What does this circuit symbol represent?',
          type: 'multi',
					option1:'open switch',
					option2:'closed switch',
          option3:'resistor',
					answer:'open switch',
					result:'',
					graphic:'../src/assets/images/openSwitch.png',
					choice:''
				},
        {
					question:'What does this circuit symbol represent?',
          type: 'multi',
					option1:'open switch',
					option2:'resistor',
          option3:'battery',
					answer:'battery',
					result:'',
					graphic:'../src/assets/images/battery.png',
					choice:''
				}	
	  ]
		//tell the program that the quiz has started
    started = true
		//add the list of questions to a new array and shuffle the questions
		questions = library
    questions.sort(function(a,b){return 0.5 - Math.random()});
		//cut the list of questions to the game length provided by the user
    questions.splice(gameLength, questions.length)
  }
	
	//function to check if the user's response matches the correct answer
	function check (response) {
		//if the response is the same as the answer, change the result to correct and add one to the total point count
		if (response == questions[i].answer) {
			result = 'Correct!'
      points += 1
		} else {
			//if the user input is incorrect, the result is wrong and this prints the correct answer as well so they know what they did wrong
			result = 'Wrong.'
      result += ' The correct answer was ' + questions[i].answer
		}
		//tell the program that the user is no longer answering a question so that it can present the option to move to the next question
    answering = false
		//return altered variables
		return result, answering, points
	}
	
	//when user clickes 'next' button - add one to index count of questions, tell the program that the user is now answering the next question. Clear result paragraph and return altered variables
	function next () {
		i += 1
    answering = true
    result = ''
    return i, result, answering
	}

	//when user wants to reset game
  function reset () {
		//tell the program they have not started the quiz
    started = false
		//tells program user is not currently answering a question
    answering = true
    valid = false
		//sets index of questions to 0 - this selects the first question in the list
    i = 0
		//resets points to 0
    points = 0
		//tells program that the user has not yet entered a valid game length
		validGameLength = false
		validAge = false
		//sets name and form room to empty text boxes
    name = ''
    formRoom = ''
		//clears result output area
    result = ''
    error = ''
    return error
  }

	//when t
	function state(choice) {
		//if the user is not answering a question, allow them to move to the next questions
		if (answering === false) {
        next()
				//otherwise, if they are answering a question, send their chosen input to be checked against the answer
        } else if (answering === true) {
				check(choice)
			}
	}

	//when a user enters a numerical input and clicks the 'next' button, this function checks if their input is valid against the set parameters for the input being taken 
  function validate( number, min, max, print ) {
		console.log (valid + '' + number + 'min' + min + 'max' + max)
    if (min > number || number > max) {
      valid = false
			error += 'The ' + print + ' you have entered is not valid. Please try again'
    } else {
			valid = true
			error = 'its TRUE'
		}
		console.log (valid + '' + number + 'min' + min + 'max' + max)
		return valid
  }
	
</script>


<h1>Electricty! (Circuits) </h1>

{#if started === false}
	{#if valid === false}
  <p>Gamelength must be a number between 1 and 10. </p>
    <label>
      Gamelength:
			{gameLength}
      <input type='range' bind:value={gameLength} min=1 max=10>
    </label>

		<label>
      Age:
      <input type='number' bind:value={age} min=0 max=130>
    </label>
      <button on:click={validate( age, 0, 130, 'age' )}>Next</button>
	{:else if valid === true}
					<input bind:value={name} placeholder="enter your name">
					<input bind:value={formRoom} placeholder="enter your form class">
				{#if (name != '' && formRoom != '')}
					<p> Hello {name} from room {formRoom}</p>
					<button id='btnStart' on:click={start}>Start Quiz</button>
			{/if}
  {/if}
  <br><br>
{:else if started === true}
<p>Name: {name}   Room: {formRoom}</p>
  {#if (i < gameLength)}
      {questions[i].question}

    {#if (questions[i].graphic != '')}
      <img src={questions[i].graphic} alt='not working'>
    {/if}

  <br>

    {#if (questions[i].type == 'multi')}
          <label>
            <input type="radio" bind:group={questions[i].choice} value={questions[i].option1}>
            {questions[i].option1}
          </label>
          <br>
          <label>
            <input type="radio" bind:group={questions[i].choice} value={questions[i].option2}>
            {questions[i].option2}
          </label>
          {#if (questions[i].option3 != '')}
            <label>
              <input type="radio" bind:group={questions[i].choice} value={questions[i].option3}>
              {questions[i].option3}
            </label>
            <br>
          {/if}
          <br>
          <br>
      {:else if (questions[i].type == 'number')}
          <input type='number' bind:value={questions[i].choice}>
          {questions[i].unit}
      {/if}

      {#if answering}
      <button id='btnCheck' on:click={state(questions[i].choice)}>
        Check
      </button>
      {:else}
      <button id='btnNext' on:click={state}>
        Next
      </button>
      {/if}
  {:else}
    <p> You are done :) </p>  
  {/if}

  {#if (result != '')}
    <p> {result} </p>
  {/if}
  <p>Points: {points}/{gameLength} </p>
{/if}
  <p>{error}</p>
	<button id='btnReset' on:click={reset}>Reset</button>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  img {
    height: 12rem;
    width: auto;
  }

  h1 {
    color: #6633FF;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
    line-height: 1.1;
    margin: 2rem auto;
    max-width: 14rem;
  }

  p {
    max-width: 14rem;
    margin: 1rem auto;
    line-height: 1.35;
  }

  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }

    p {
      max-width: none;
    }
  }

  input[type=number] {
    width: 40px;
  }

</style>
