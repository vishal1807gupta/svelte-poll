<script>
	import Header from "./components/Header.svelte";
	import Footer from "./components/footer.svelte";
	import PollList from "./components/Poll_list.svelte";
	import Tabs from "./shared/tabs.svelte";
	import CreatePollForm from "./components/CreatePollForm.svelte";

	let items = ['Current Polls','Add New Poll'];
	let activeItem = 'Current Polls';

	// let polls = [
	// 	{
	// 		id:1,
	// 		question : 'Python or Javascript?',
	// 		answerA : 'Python',
	// 		answerB : 'Javascript',
	// 		votesA : 9,
	// 		votesB : 15
	// 	},
	// ]

	const tabChange = (e)=>{
		activeItem = e.detail;
	}

	const handleAdd = (e)=>{
        // const poll = e.detail;
		// polls = [poll,...polls];
		// console.log(polls);
		activeItem='Current Polls';
	}

	// const handleVote = (e)=>{
	// 	const {option,id} = e.detail;
	// 	let copiedPolls = [...polls];
	// 	let upvotePoll = copiedPolls.find((poll)=>poll.id==id);
	// 	if(option=='a')upvotePoll.votesA++;
	// 	else upvotePoll.votesB++;
	// 	polls = copiedPolls;
	// }
</script>

<Header/>
<main>
	<Tabs on:tabChange={tabChange} {activeItem} {items}/>
	{#if activeItem=== 'Current Polls'}
	 <!-- <PollList {polls} on:vote={handleVote}/> -->
	 <!-- <PollList on:vote={handleVote}/> -->
	 <PollList/>
	 {:else if activeItem=== 'Add New Poll'}
	 <CreatePollForm on:add={handleAdd}/>
	 {/if}
</main>
<Footer/>

<style>
	main{
		max-width: 960px;
		margin : 40px auto;
	}
</style>