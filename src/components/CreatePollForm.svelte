<script>
import PollStore from "../Stores/PollStore.js"
import { createEventDispatcher } from "svelte"
import Button from "../shared/Button.svelte"
  
  const dispatch = createEventDispatcher();
  let fields = {question: '', answerA: '', answerB: ''}
  let errors = {question: '', answerA: '', answerB: ''}
  let valid = false;
  const submitHandler = () => {
      valid = true;
    //   validate question
    if(fields.question.trim().length < 5 ){
        valid = false;
        errors.question = "Question must be at least 5 characters long";
    } else {
        errors.question = '';
    }
    // validate answer a
    if(fields.answerA.trim().length < 1 ){
        valid = false;
        errors.answerA = "Answer A cannot be empty";
    } else {
        errors.answerA = '';
    }
    // validate answer b
    if(fields.answerB.trim().length < 1 ){
        valid = false;
        errors.answerB = "Answer B cannot be empty";
    } else {
        errors.answerB = '';
    }

    // Add new poll
    if(valid){
        const poll = {...fields, votesA: 0, votesB: 0, id: Math.random()}
        PollStore.update(currentPolls => {
            return [poll, ...currentPolls];
        })
        dispatch('add');
    }
  }
</script>
<form on:submit|preventDefault={submitHandler}>
<div class="form-field">
<label for="question">Question:</label>
<input type="text" id="question" bind:value={fields.question} placeholder="Question">
<div class="error">{errors.question}</div>
</div>
<div class="form-field">
<label for="answer-a">Answer A:</label>
<input type="text" id="answer-a" bind:value={fields.answerA} placeholder="Answer A">
<div class="error">{errors.answerA}</div>
</div>
<div class="form-field">
<label for="answer-b">Answer B:</label>
<input type="text" id="answer-b" bind:value={fields.answerB} placeholder="Answer B">
<div class="error">{errors.answerB}</div>
</div>
<Button type="success" flat=true>Create Poll</Button>
</form>

<style>
form {
    width: 400px;
    margin: 0 auto;
    text-align: center;
}

.form-field {
    margin: 18px auto;
}

input {
    width: 100%;
    border-radius: 4px;
    outline: none;
    padding: 9px 14px;
}

label {
    margin: 10px auto;
    text-align: left;
}

.error {
    font-size: 12px;
    font-weight: bold;
    color: #d91b42;
    text-align: left;
}

</style>