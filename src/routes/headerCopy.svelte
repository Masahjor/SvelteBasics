<!-- this is a comment -->

<!-- Script tag up top -->
<script lang="ts">

    //* this is a prop
    let { 
        name, fake_name = 'Purple' 
    } : {
        name: string;
        fake_name?: string;
    } = $props();
    //* $ i syntaxen hedder Runes, DOLLARTEGN -> HVAD DU BRUGER -> FUNKTION
    //* man kan fx. skabe props med $props, $state til at skabe state. Man kan også bruge derive og effect og meget mere.

</script>

<!-- HTML in the middle -->
<h1>Hello {name}, this is Header</h1>
<h2 class="name_title">{name.replaceAll("r", "w")}</h2>
<h2 class="fake_name_title">is not {fake_name}</h2>

<!-- CSS at the bottom -->
<style>
    .name_title {
        color: green;
    }

    .fake_name_title {
        color: purple;
    }
</style>
