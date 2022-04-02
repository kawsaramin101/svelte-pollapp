<script>
    import { slide } from 'svelte/transition';
    import { tweened } from 'svelte/motion';
    
    import Header from "./components/header.svelte";
    import Footer from './components/Footer.svelte';
    import CreatePollForm from './components/CreatePollForm.svelte';
    import PollList from './components/PollList.svelte';
    import Tabs from './shared/Tabs.svelte';

    //tabs
    let items = ["Current Polls", "Add New Item"];
    let activeItem = "Current Polls";

    function tabChange(event) {
        activeItem = event.detail;
    };

    function addPoll(event) {
        activeItem = "Current Polls";
    };
    
    const value = tweened(0);
    

</script>


<Header />
<main>
    <Tabs {items} {activeItem} on:tabChange={tabChange} />
    {#if activeItem === "Current Polls" }
    <div transition:slide={{axis: "x"}}>
        <PollList />
    </div>
    {:else if activeItem === "Add New Item" }
    <div transition:slide={{axis: "x"}}>
        <CreatePollForm on:addPoll={addPoll} />
    </div>
    {/if }
</main>
<Footer />
<button on:click={() => value.set(1)}>{$value}</button>

<style>
    main {
        width: 100%;
        max-width: 960px;
        margin: 40px auto;
    }
</style>