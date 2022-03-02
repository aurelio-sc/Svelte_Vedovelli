<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

   export let title="Olá eu sou o Comp1!";
   export let subtitle="Subtitle do Compo1."
   export let membersOnly = false;
   export let id = 0;

   const clickHandler = () => dispatch('cardClicked', { id }); //cria um evento chamado cardClicked e o que acontece depois.
                                                               //com o evento criado, ele pode ser usado no App.svelte

</script>



<a href="https://www.google.com"  on:click|preventDefault={clickHandler}> <!-- |preventDefault não deixa o link funcionar como deveria quando clicado. -->
    <div class="card">
        <h1> {title} </h1>
        <h2> {subtitle} </h2>
        <p>lorem ipsum dolor sit amet</p>
        <p>lorem ipsum dolor sit amet</p>
        <p>----</p>

        {#if membersOnly}                                 <!--Lógica no HTML do componente!-->
        <p>Isto aparece se membersOnly for true</p>
        {:else}
        <p>Isso aparece se membersOnly for false</p>
        {/if}
    </div>
</a>