

<script lang="ts">
    import { parse, lexer } from "$lib/markedjs/marked";
    import { onMount } from "svelte";

    // Markdown Components
    import Heading1 from "./md/Heading1.svelte";
    import List from "./md/List.svelte";
    import Paragraph from "./md/Paragraph.svelte";
    import Space from "./md/Space.svelte";

    export let markdown = "";

    interface ComponentWithMdContent {
        component: typeof Heading1 | typeof List; // | typeof Paragraph | typeof Space ........
        content: string;
    }

    $: components = componentRenderer(markdown);

    function componentRenderer(markdown:string): Array<ComponentWithMdContent> {
        let newComponents = [];

        const markdownAST = lexer(markdown);
        console.log(markdownAST);

        for (let node of markdownAST) {

            if (node.type == "heading") {
                const content = node?.text ?? "";
                newComponents.push(
                    {component: Heading1, content: content}
                );
            }
            
        }
        return newComponents;
    }   
</script>

{#each components as c}
  <svelte:component this={c.component} content={c.content} />
{/each}