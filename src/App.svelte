<script>
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
	
  function start() {
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

    started = true
		questions = library
    questions.sort(function(a,b){return 0.5 - Math.random()});
    questions.splice(gameLength, questions.length)
    questions[i].choice = ''
  }

	let i = 0
	let question = questions.at[i]
  let answering = true
  let complete = false
	
	function check (response) {
		if (response == questions[i].answer) {
			result = 'Correct!'
      points += 1
		} else {
			result = 'Wrong.'
      result += ' The correct answer was ' + questions[i].answer
		}
    answering = false
		return result, answering, points
	}
	
	function next () {
		i += 1
    answering = true
		console.log('i = ' + i)
    result = ''
    questions[i].choice = ''
    return result, answering
	}

  function reset () {
    started = false
    answering = true
    i = 0
    points = 0
		gameLength = 3
		valid = false
    name = ''
    formRoom = ''
    result = ''
  }

	function state(choice) {
		if (answering === false) {
        next()
        } else if (answering === true) {
				check(choice)
			}
	}

  function validate(number, min, max) {
		console.log (number + 'min' + min + 'max' + max)
    if (min > number || number > max) {
      valid = false
			console.log(valid)
			error += 'Gamelength is not valid. Try again'
    } else {
			valid = true
			error = ''
		}
		return valid
  }
	
</script>

<h1>Electricty! (Circuits) </h1>

{#if started === false}
  {#if valid === false}
  <p>Gamelength must be a number between 1 and 11. </p>
    <label>
      Gamelength:
      <input type='number' bind:value={gameLength}>
      <button on:click={validate(gameLength, 1, 11)}>Next</button>
    </label>
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
