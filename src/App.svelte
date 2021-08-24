<script>
	let input = ''
	let choice = ''
	let result = ''
  let points = 0
  let name = ''
  let formRoom = ''
	
	let questions = [
				{
					question:'Does current split or stay constant through a series 			circuit?',
          type: 'multi',
					option1:'same',
					option2:'splits',
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
					graphic:'../src/assets/circuit1.png',
					choice:''
				},
        {
					question:'Does voltage stay constant or split in a parallel circuit?',
          type: 'multi',
					option1:'same',
					option2:'splits',
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
					result:'',
					graphic:'',
					choice:''
				},
        {
					question:'An electric field is set up between parallel plates. A proton is placed between the plates, will it travel with or against the field lines?',
          type: 'multi',
					option1:'with',
					option2:'against',
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
					answer:'against',
					result:'',
					graphic:'',
					choice:''
				}
			
	]
	
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
		console.log('function is done. result is ' + result + 'answering is ' + answering)
		return result, answering, points
	}
	
	function next () {
		console.log('function next running')
		i += 1
    answering = true
		console.log('i = ' + i)
    result = ''
    return result, answering
	}

  function reset () {
    answering = true
    i = 0
    points = 0
    name = ''
    formRoom = ''
    input = ''
    choice = ''
    result = ''
		console.log(answering + i + points)
  }

	function state(choice) {
		console.log('function state running. answering = ' + answering + 'complete is ' + complete)
		if (answering === false) {
        next()
        } else if (answering === true) {
				check(choice)
			}
	}
	
</script>

<h1>Electricty! </h1>

<input bind:value={name} placeholder="enter your name">

<input bind:value={formRoom} placeholder="enter your form class">

{#if name != '' && formRoom != ''}
  <p> Hello {name} from room {formRoom}</p>
{/if}
<br><br>
{#if (i < questions.length)}
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
    <button id='btnCheck' on:click={reset}>Reset</button>
  
{/if}

{#if (result != '')}
	<p> {result} </p>
{/if}
<p>Points: {points}/{questions.length} </p>


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
