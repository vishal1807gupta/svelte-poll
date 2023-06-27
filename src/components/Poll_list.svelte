<script>
    // import {onMount ,onDestroy} from 'svelte';
    import {fade, slide , scale} from 'svelte/transition';
    import {flip} from 'svelte/animate';
    import PollDetails from "./PollDetails.svelte";
    import PollStore from "../stores/PollStore.js";
    // export let polls = [];

    // const unsub = PollStore.subscribe((data)=>{
    //   polls = data;
    // }) // This function update the pollstore as there is any change in the data and also return the unsubscription function which we invoke to unsubscribe or remove our data to prevent memory leak

    // onMount(()=>{
    //   console.log('component mounted');
    // })

    // onDestroy(()=>{
    //   unsub();
    //   console.log('component destroyed');
    // })

</script>

<div class="poll-list">
    <!-- {#each polls as poll(poll.id)} -->
    <!-- This $PollStore automatically subscribe and unsubscribe the pollstore as component is mounted and destroyed respectively and also provide the data which is equivalent to polls which we stored in it -->
    {#each $PollStore as poll(poll.id)} 
       <!-- <div><PollDetails {poll} on:vote/></div> -->
       <div in:fade out:scale|local animate:flip={{duration : 500}}><PollDetails {poll}/></div> 
       <!-- local indicate if there is only individual item removed out then out:scale -->
    {/each}
</div>

<style>
  .poll-list{
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>