<!-- this is a comment -->

<!-- Script tag up top -->
<script lang="ts">
    import { createState, NameState } from './state.svelte';

    //* this is a prop
    let { 
        name
    } : {
        name: string;
    } = $props();
    //* $ i syntaxen hedder Runes, DOLLARTEGN -> HVAD DU BRUGER -> FUNKTION
    //* man kan fx. skabe props med $props, $state til at skabe state. Man kan også bruge derive og effect og meget mere.

    const myState = createState();
    const myStateTwo = new NameState();

</script>

<!-- HTML in the middle -->
<div>
    <h1>
        {name ? name : 'User'}'s Form
    </h1>
    <button onclick={myState.up}>{myState.value}</button>
    <button onclick={() => myStateTwo.up()}>{myStateTwo.value}</button>

</div>

<!-- CSS at the bottom -->
<style>

</style>
