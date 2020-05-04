<script>
// import {createEventDispatcher } from "svelte"
import Card from "../shared/Card.svelte"
import PollStore from "../Stores/PollStore.js"
import Button from "../shared/Button.svelte"
import { tweened } from "svelte/motion" 
export let poll;
// const dispatch = createEventDispatcher();

// Reactive values
$: totalVotes = poll.votesA + poll.votesB;
$: percentA = Math.floor(100 / totalVotes * poll.votesA) || 0;
$: percentB = Math.floor(100 / totalVotes * poll.votesB) || 0;

// Tweened percentages
const tweenedA = tweened(0);
const tweenedB = tweened(0);
$: tweenedA.set(percentA);
$: tweenedB.set(percentB);

// console.log($tweenedA, $tweenedB);

// Votes handler
const handleVote = (option, id) => {
    // dispatch('vote', {option, id});
    PollStore.update(currentPolls => {
        let copiedPolls = [...currentPolls];
		let upvotedPoll = copiedPolls.find((poll) => poll.id === id);
		if(option === "a"){
			upvotedPoll.votesA++;
		}
		if(option === "b"){
			upvotedPoll.votesB++;
		}
		return copiedPolls
    })
}

// Deleteting a poll
const handleDelete = (id) => {
    PollStore.update(currentPolls => {
        return currentPolls.filter(poll => poll.id !== id);
    })
}

</script>

<Card>
<div class="poll">
  <h3>{poll.question}</h3>
  <p>Total votes: {totalVotes}</p>
  <div class="answer" on:click={() => handleVote('a', poll.id)}>
  <div class="percent percent-a" style="width: {$tweenedA}%"></div>
  <span>{poll.answerA} ({poll.votesA})</span>
  </div>

  <div class="answer" on:click={() => handleVote('b', poll.id)}>
  <div class="percent percent-b" style="width: {$tweenedB}%"></div>
  <span>{poll.answerB} ({poll.votesB})</span>
  </div>
  <div class="delete">
  <Button flat=true on:click={() => handleDelete(poll.id)}>Delete</Button>
  </div>
</div>
</Card>

<style>
h3 {
    margin: 0 auto;
    color: #555;
}
p {
    margin: 6px;
    font-size: 14px;
    color: #aaa;
    margin-bottom: 30px;
}
.answer {
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
}
.answer:hover {
    opacity: .6;
}
span {
    display: inline-block;
    padding: 10px 20px;
}
.percent {
    position: absolute;
    height: 100%;

}
.percent-a {
    background: rgba(217,27,66,.2);
    border-left: 4px solid #d91b42;
}
.percent-b {
    background: rgba(69, 196, 150, .2);
    border-left: 4px solid #45c496;
}
.delete {
    margin-top: 30px;
    text-align: center;
}
</style>