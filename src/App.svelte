<script>
	let input = ''
	let choice = ''
	let result = ''
	
	let questions = [
				{
					question:'Does current split or stay constant through a series 			circuit?',
					option1:'same',
					option2:'splits',
					answer:'same',
					result:'',
					graphic:'',
					choice:''
				},
				{
					question:'Does voltage stay constant or split in a series circuit?',
					option1:'same',
					option2:'splits',
					answer:'splits',
					result:'',
					graphic:'',
					choice:''
				},
        {
					question:'What is the voltage across the lightbulb in this circuit?',
					option1:'4V',
					option2:'6V',
					answer:'4V',
					result:'',
					graphic:'../src/assets/circuit1.png',
					choice:''
				}
			
	]
	
	let i = 0
	let question = questions.at[i]
  let answering = true
	
	function check (response) {
		if (response == questions[i].answer) {
			result = 'correct'
		} else {
			result = 'wrong'
      result += ' the correct answer was ' + questions[i].answer
		}
    answering = false
		console.log('function is done. result is ' + result + 'answering is ' + answering)
		return result, answering
	}
	
	function next () {
		console.log('function next running')
		i += 1
    answering = true
		console.log('i = ' + i)
    result = ''
    return result, answering
	}

	function state(choice) {
		console.log('function state running. answering = ' + answering)
		if (answering === false) {
				next ()
			} else if (answering === true) {
				check(choice)
			}
	}
	
	
</script>

<h1>Electricty! </h1>

{#if (i < questions.length)}
    {questions[i].question}

  {#if (questions[i].graphic != '')}
    <img src={questions[i].graphic} alt='not working'>
  {/if}
        <br>
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
<p>
	{result}
</p>


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
</style>
