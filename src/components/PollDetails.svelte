<script>
import {createEventDispatcher } from "svelte"
import Card from "../shared/Card.svelte"
export let poll;
const dispatch = createEventDispatcher();

// Reactive values
$: totalVotes = poll.votesA + poll.votesB;
$: percentA = Math.floor(100 / totalVotes * poll.votesA);
$: percentB = Math.floor(100 / totalVotes * poll.votesB);

// Votes handler
const handleVote = (option, id) => {
    dispatch('vote', {option, id});
}

</script>

<Card>
<div class="poll">
  <h3>{poll.question}</h3>
  <p>Total votes: {totalVotes}</p>
  <div class="answer" on:click={() => handleVote('a', poll.id)}>
  <div class="percent percent-a" style="width: {percentA}%"></div>
  <span>{poll.answerA} ({poll.votesA})</span>
  </div>

  <div class="answer" on:click={() => handleVote('b', poll.id)}>
  <div class="percent percent-b" style="width: {percentB}%"></div>
  <span>{poll.answerB} ({poll.votesB})</span>
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
</style>