<script lang="ts">
    export let content = "";

    $: paragraph = parseParagraph(content)

    function parseParagraph(content:string) : string {
        content = content.replace(/(\r\n|\r|\n)/g, '<br>');
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
    p {
        color: red;
        font-family: "Inconsolata", monospace;
    }
</style>

<p>{@html paragraph}</p>