<script>
	let input = ''
	let choice = ''
	let result = ''
	
	let questions = [
				{
					question:'Does current split or stay constant through a series circuit?',
					option1:'Same',
					option2:'Splits',
					answer:'Same',
					result:'',
					choice:''
				},
				{
					question:'Does voltage stay constant or split in a series circuit?',
					option1:'Same',
					option2:'Splits',
					answer:'Splits',
					result:'',
					choice:''
				}
	]
	let i = 1
	let question = questions.at[i]
	
	function check (response) {
		if (response == questions[i].answer) {
			result = 'correct'
		} else {
			result = 'wrong'
		}
		console.log('function is done. result is ' + result)
		result += ' the correct answer was ' + questions[i].answer
		return result
	}
	
</script>

<h1>Electricty! </h1>

<p>
	hello there. Please bare with the code is not done yet.
</p>

<!-- {#if (i < questions.length)} -->
  {questions[i].question}
      <label>
        <input type="radio" bind:group={questions[i].choice} value={questions[i].option1}>
        {questions[i].option1}
      </label>
      <br>
      <label>
        <input type="radio" bind:group={questions[i].choice} value={questions[i].option2}>
        {questions[i].option2}
      </label>

<label>
<button on:click={check(questions[i].choice)}>
	Check answer
	</button>
</label>

<p>
	{result}
</p>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }

  img {
    height: 16rem;
    width: 16rem;
  }

  h1 {
    color: #ff3e00;
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
