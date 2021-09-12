<script>
  //create empty variables to set up page
	let choice = ''
	let result = ''
  let points = 0
  let name = ''
  let formRoom = ''
  let gameLength = 3
  let started = false
  let questions = []
  let valid = false
	let error = ''
	let i = 0
	let question = questions.at[i]
  let answering = true
  let complete = false
	let age = ''
	let letter = false

	//create a library with a list of question options
  let library = [
				{
				 	question:'Does current split or stay constant through a series 			circuit?',
          type: 'multi',
				  option1:'same',
					option2:'splits',
          option3: '',
					answer:'same',
					result:'',
					graphic:'',
          graphicClass: '',
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
          graphicClass: '',
					choice:''
				},
        {
					question:'What is the voltage across the lightbulb in this circuit?',
          type: 'number',
					answer:'4',
          unit: 'Volts',
					result:'',
					graphic:'../src/assets/images/circuit1.png',
          graphicClass:'large',
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
          graphicClass: '',
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
          graphicClass: '',
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
          graphicClass: '',
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
          graphicClass: '',
					choice:''
				},
        {
					question:'The voltmeter reads 4.0V. What is the current around the circuit? Hint: V = IR',
          type: 'number',
					answer:'0.8',
          unit: 'Amps',
					result:'',
					graphic:'../src/assets/images/circuit2.png',
          graphicClass: 'large',
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
          graphicClass: 'small',
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
          graphicClass: 'small',
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
          graphicClass: 'small',
					choice:''
				}	
	  ]
	
  //start function. when the start button is clicked, generate the library of questions 
  function start() {
		console.log('function start')
		//tell the program that the quiz has started
    started = true
		//add the list of questions to a new array and shuffle the questions
		questions = library.slice()
    questions.sort(function(a,b){return 0.5 - Math.random()});
		//cut the list of questions to the game length provided by the user
    questions.splice(gameLength, questions.length)
  }
	
	//function to check if the user's response matches the correct answer
	function check (response) {
    if (response != '') {
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
            error = ''
					} else {
						error = 'Please enter an answer'
					}
		
		//return altered variables
		return result, answering, points
	}
	
	//when user clicks 'next' button - add one to index count of questions, tell the program that the user is now answering the next question. Clear result paragraph and return altered variables
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
		//sets index of questions to 0 - this selects the first question in the list
    i = 0
		//resets points to 0
    points = 0
		//tells program that the user has not yet entered a valid age
		valid = false
		letter = false
		//sets name and form room to empty text boxes
    name = ''
    formRoom = ''
		//clears result output area
    result = ''
    error = ''
    return error, name, formRoom
  }

	//when a user enters a numerical input and clicks the 'next' button, this function checks if their input is valid against the set parameters for the input being taken 
  function validate( number, min, max, rec, print ) {
    if ((number == '') || (number < min || number > max)) {
      valid = false
      error = 'The ' + print + ' you have entered is not valid. Please try again'			
    } else if (rec > number) {
			error = 'You are too young!'   
    } else {
			valid = true
			error = ''
		}
		return valid
  }

  function validName(text) {
		console.log(text)
      for (let i = 0; i < text.length; i++) {
				console.log(text.charAt(i))
				if ((text.charAt(i)).toLowerCase() != (text.charAt(i)).toUpperCase()) {
					letter = true
					error = ''
					console.log('true')
				} else {
					letter = false
					i -= 1
					error = 'The name you have entered is not valid. Try again. Name must be comrpised of only letters.'
					console.log('false')
				}
			}
    return letter
  }
	
</script>

<h1>Electricty! (Circuits) </h1>

<!-- if the user has not started the quiz or entered a valid age, show them the start page with an option to input a game length and an age -->
{#if started === false}
	{#if valid === false}
    <!-- slider connected to game length input offers numbers between 1 and 10 -->
    <label>
      Gamelength:
			{gameLength}
      <input type='range' bind:value={gameLength} min=1 max=10>
    </label>
    <!-- number input for user's age-->
		<label>
      Age:
      <input type='number' bind:value={age} min=0 max=130>
    </label>
    <!-- 'next' button - checks that user has entered a valid age - if yes it allows them to move to the next screen, if not it prints an error message -->
      <button on:click={validate( age, 0, 130, 8, 'age' )}>Next</button>
	{:else if valid}
<!--   if the user has entered a valid age, offer input area for name and form room values      -->
				{#if letter === false}
						<input bind:value={name} placeholder="enter your name">
						<input bind:value={formRoom} placeholder="enter your form class">
							{#if (name != '' && formRoom != '')}
								<button on:click={validName(name)}>Next</button>
							<!-- if the user has entered a value into both the name and form room input areas, greet the user and give them the option to start the quiz by presenting the start button -->
							{:else if (name == '' || formRoom == '')}
								<p> Please enter a name and form room </p>
							{/if}
				{:else if letter === true}
						<p> Hello {name} from room {formRoom}</p>
						<button id='btnStart' on:click={start}>Start Quiz</button>
				{/if}
  {/if}
  <br><br>
{:else if started === true}
<!-- if the user has started the quiz, greet them with their name and form room -->
<p>Welcome {name}!  Room: {formRoom}</p>
<!-- if the index on questions is less than the specified game length, present the question to the user -->
  {#if (i < gameLength) }
      {questions[i].question}

    <!-- if the question has a graphic (image) associated with it - show the image here -->
    {#if (questions[i].graphic != '')}
      <img class={questions[i].graphicClass} src={questions[i].graphic} alt='circuit'>
    {/if}

  <br>

  <!-- if the question is multi choice, present the options as radio buttons. -->
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
          <!-- if there is a third option, present it here -->
          {#if (questions[i].option3 != '')}
            <label>
              <input type="radio" bind:group={questions[i].choice} value={questions[i].option3}>
              {questions[i].option3}
            </label>
            <br>
          {/if}
          <br>
          <br>
      <!-- if the question requires a numerical response, present a number input box with the unit next to it -->
      {:else if (questions[i].type == 'number')}
          <input type='number' bind:value={questions[i].choice}>
          {questions[i].unit}
      {/if}

    <!-- while the user is answering a question, present the option for them to check their response with a 'check' button -->
      {#if answering}
      <button id='btnCheck' on:click={check(questions[i].choice)}>
        Check
      </button>
      <!-- if they are not currently answering a question, allow them to move to the next question with a 'next' button -->
      {:else}
      <button id='btnNext' on:click={next}>
        Next
      </button>
      {/if}
  <!-- if they have done the number of questions specified by game length, tell the user they have finsihed the quiz and how they can play again -->
  {:else}
    <p> You are done :). To play again - click reset. </p>  
  {/if}

<!-- paragraph with result which is what tells the user if they have answered the question correctly or not and alerts them of the correct answer -->
	<p> {result} </p>

<!-- tells the user how many points they have - points are added when a correct answer is guessed -->
  <p>Points: {points}/{gameLength} </p>
{/if}
<!-- if the user has entered an invalid input, this alerts them of what they have done wring with a friendly message -->
	<p>{error}</p>

<!-- reset button - this is shown at all times so the user can restart at any stage -->
	<button id='btnReset' on:click={reset}>Reset</button>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  .large {
    height: 12rem;
    width: auto;
  }

  .small {
    height: 6rem;
    width: auto
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
