
<script lang="ts">
    import Main from "$lib/components/Main.svelte";
    import { parse } from "$lib/markedjs/marked";
    import { onMount } from "svelte";

    const components = [
        { component: Main, props: { text: 'Hello World' }},
        { component: Main, props: { text: 'This is a paragraph.' }},
        { component: Main, props: { src: '/img.png', alt: 'Image' }},
    ];

    async function renderMarkdown() {
      const markdownText = (document.getElementById('markdown-input') as HTMLTextAreaElement).value;
      const html = await parse(markdownText);
      (document.getElementById('html-output') as HTMLDivElement).innerHTML = html;
    }

    onMount( () => {
        renderMarkdown();
    });
</script>

<textarea id="markdown-input" rows="10" cols="50" on:input={renderMarkdown}>
# Hello World

This is some **bold** text and some *italic* text.

- List item 1
- List item 2
</textarea>

<div id="html-output" style="border: 1px solid #ccc; padding: 10px;"></div>

{#each components as { component: Comp, props }}
  <svelte:component this={Comp} />
{/each}