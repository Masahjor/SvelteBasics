<script lang="ts">
    import Header from './Header.svelte'
    let name = $state('Braingreen');
    let status: 'OPEN' | 'CLOSED' = $state('OPEN');
    let full_name = $derived(name + " " + 'Grønsen')

    // function toggle() {
    //     status = status === "OPEN" ? "CLOSED" : "OPEN";
    // }
    function onclick() {
        status = status === "OPEN" ? "CLOSED" : "OPEN";
    }
</script>

<!-- this is a prop. examples: prop={prop_value}, name={name} -->
<Header {name} />

<h2>{full_name}</h2>

<input type="text" bind:value={name} />

<p>The store is now {status}</p>
<!-- <button {onclick}>Toggle Status</button> -->
<button
    onclick={() => {
        status = status === "OPEN" ? "CLOSED" : "OPEN";
    }}>Toggle Status</button
>
