
<script>
    import Main from "$lib/components/Main.svelte";

    const components = [
    { component: Main, props: { text: 'Hello World' }},
    { component: Main, props: { text: 'This is a paragraph.' }},
    { component: Main, props: { src: '/img.png', alt: 'Image' }},
  ];
</script>

{#each components as { component: Comp, props }}
  <svelte:component this={Comp} />
{/each}