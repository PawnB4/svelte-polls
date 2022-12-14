<script>
  import CreatePollForm from "./lib/CreatePollForm.svelte";
  import Footer from "./lib/Footer.svelte";
  import Header from "./lib/Header.svelte";
  import PollList from "./lib/PollList.svelte";
  import Tabs from "./shared/Tabs.svelte";

  // Tabs

  let items = ["Current Polls", "Add new Poll"];
  let activeItem = "Current Polls";
  const tabChange = (e) => {
    activeItem = e.detail;
  };

  // Polls

  let polls = [
    {
      id: 1,
      question: "Python or JavaScript?",
      answerA: "Python",
      answerB: "JavaScript",
      votesA: 19,
      votesB: 13,
    },
  ];

  const handleAdd = (e) => {
    const poll = e.detail;
    polls = [poll, ...polls];
    console.log(polls);
    activeItem = "Current Polls";
  };
</script>

<Header />
<main>
  <Tabs {items} {activeItem} on:tabChange={tabChange} />
  {#if activeItem === "Current Polls"}
  <PollList {polls}/>
  {:else if activeItem === "Add new Poll"}
    <CreatePollForm on:add={handleAdd} />
  {/if}
</main>
<Footer />

<style>
  main {
    max-width: 80%;
    margin: 40px auto;
  }
</style>
