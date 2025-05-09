<script lang="ts">
    export let content = "";

    $: heading1 = parseHeading1(content)

    function parseHeading1(content:string) : string {
        return content
    }

</script>

<svelte:head>
    <link
      href="https://fonts.googleapis.com/css2?family=Inconsolata:wght@400;700&display=swap"
      rel="stylesheet"
    />
</svelte:head>

<style>
    h1 {
        color: yellowgreen;
        font-family: "Inconsolata", monospace;
    }
</style>

<h1>{heading1}</h1>