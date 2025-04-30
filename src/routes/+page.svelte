<script lang="ts">
	import { fly } from 'svelte/transition';
    import Header from './Header.svelte'

    let formState = $state({
        answers: {},
        step: 0,
        error: ''
    });

    $inspect(formState.step);

    const QUESTIONS = [
        { 
            question: "What's your name?", 
            id: "name", 
            type: "text" 
        },
        { 
            question: "What's your birthday?", 
            id: "birthday", 
            type: "date"
        },
        {
            question: "What's your favourite colour?",
            id: "colour",
            type: 'color'
        }
    ];

    function nextStep(id: string) {
        if(formState.answers[id]) {
            formState.step += 1;
            formState.error = '';
        } else {
            formState.error = 'Please fill out the field';
        }
    }

    // Kører onMount
    $effect(() => {
        console.log('on mounted');
        return () => {
            // når unmounted eller er destrueret
            // før effect kører igen
            console.log('on unmounted');
        }
    });

    $effect(() => {
        // kører hver gang formState.step ændres
        // console.log('formState', formState.step);
        // DON'T create state based oFF other state, in effect.
        // use $derived() instead
        return () => {
            // før effect kører igen
            // console.log('before formState.step re-runs', formState.step);
        }
    });

</script>

<Header name={formState.answers.name} />


<main>
    {#if formState.step >= QUESTIONS.length}
        <p>Thank you!</p>
    {:else}
        <p>Step: {formState.step + 1}</p>
    {/if}

    {#each QUESTIONS as question, index (question.id)}
        {#if formState.step === index}
        <div 
            in:fly={{ x: 200, duration: 200, opacity: 0, delay: 200 }} 
            out:fly={{ x: -200, duration: 200, opacity: 0 }}
            >
            {@render formStep(question)}
        </div>
        {/if}
    {/each}
    <!-- {#each QUESTIONS as {id, question, type} (id)}
        {@render formStep({question, id, type})}
    {/each} -->


    {#if formState.error}
        <p class="error">{formState.error}</p>
    {/if}

</main>



<!-- {JSON.stringify(formState)} -->

{#snippet formStep({ question, id, type }: {
    type: string;
    id: string;
    question: string;
})}
    <article>
        <div>
            <label for={id}>{question}</label>
            <input {type} {id} bind:value={formState.answers[id]}/>
        </div>
        <button onclick={() => nextStep(id)}>Next</button>
    </article>
{/snippet}

<!-- CSS -->
<style>
    /* man kan skrive :global(X) på et tag eller klasse for at gøre det globalt, ellers forbliver CSS inde for deres filer. Fx: :global(div) {... */
    div {
        background: invisible;
    }
    .error {
        color: red;
    }
</style>