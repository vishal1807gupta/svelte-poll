<script>
//    import {createEventDispatcher} from "svelte";
   import Card from "../shared/card.svelte";
   import PollStore from "../stores/PollStore";
   import Button from "../shared/button.svelte";
   import {tweened} from 'svelte/motion';
   export let poll;
   $: totalVotes = poll.votesA + poll.votesB;
   $: percentA = Math.floor(100/totalVotes*poll.votesA) || 0;
   $: percentB = Math.floor(100/totalVotes*poll.votesB) || 0;

//    let dispatch = createEventDispatcher();

   const handleVote = (option,id)=>{
        // dispatch('vote',{option,id});
		PollStore.update(currentPolls=>{
            let copiedPolls = [...currentPolls];
            let upvotePoll = copiedPolls.find((poll)=>poll.id==id);
            if(option=='a')upvotePoll.votesA++;
            else upvotePoll.votesB++;
            return copiedPolls;
        })
   }
   const handleDelete = (id)=>{
        // dispatch('vote',{option,id});
		PollStore.update(currentPolls=>{
            let copiedPolls = [...currentPolls];
            let upvotePoll = copiedPolls.filter((poll)=>poll.id!=id);
            return upvotePoll;
        })
   }

   const tweenedA = tweened(0);
   const tweenedB = tweened(0);

   $:tweenedA.set(percentA);
   $:tweenedB.set(percentB);
</script>

<Card>
<div class="poll">
    <h3>{poll.question}</h3>
    <p>TotalVotes : {totalVotes}</p>
    <div class="answer" on:click={()=>{handleVote('a',poll.id)}}>
        <div class="percent percent-a" style="width:{$tweenedA}%"></div>
        <span>{poll.answerA} ({poll.votesA})</span>
    </div>
    <div class="answer" on:click={()=>{handleVote('b',poll.id)}}>
        <div class="percent percent-b" style="width:{$tweenedB}%"></div>
        <span>{poll.answerB} ({poll.votesB})</span>
    </div>
    <div class="delete">
        <Button flat={true} on:click={()=>{handleDelete(poll.id)}}>Delete</Button>
    </div>
</div>
</Card>

<style>
    h3{
        margin: 0 auto;
        color: #555;
    }
    p{
        margin-top: 6px;
        font-size: 14px;
        color: #aaa;
        margin-bottom: 38px;
    }
    .answer{
        background: #fafafa;
        cursor: pointer;
        margin: 10px auto;
        position: relative;
    }
    .answer:hover{
        opacity: 0.6;
    }
    span{
        display: inline-block;
        padding: 10px 20px;
    }
    .percent{
        height:100%;
        box-sizing : border-box;
        position : absolute;
    }
    .percent-a{
        border-left:4px solid #d91b42;
        background: rgba(217,27,66,0.2);
    }
    .percent-b{
        border-left:4px solid #45c496;
        background: rgba(69,196,150,0.2);
    }
    .delete{
        margin-top: 30px;
        text-align: center;
    }
</style>