

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
        component: Heading1 | List | Paragraph
    }

    class Heading1WithMdContent implements ComponentWithMdContent{
        component:any = Heading1
        content: string
        constructor(t: string) {
            this.content = t
        }
    }

    class ParagraphWithMdContent implements ComponentWithMdContent{
        component:any = Paragraph
        content: string
        constructor(t: string) {
            this.content = t
        }
    }

    $: components = componentRenderer(markdown);

    function componentRenderer(markdown:string): Array<ComponentWithMdContent> {
        let newComponents: Array<ComponentWithMdContent> = [];

        const markdownAST = lexer(markdown);
        console.log(markdownAST);

        for (let node of markdownAST) {

            if (node.type == "heading") {
                const content = node?.text ?? "";
                const newComponent = new Heading1WithMdContent(content)
                newComponents.push(
                    newComponent
                );
            }

            if (node.type == "paragraph") {
                const content = node?.text ?? "";
                const newComponent = new ParagraphWithMdContent(content)
                newComponents.push(
                    newComponent
                );
            }
            
        }
        return newComponents;
    }   
</script>

{#each components as c}

  {#if c instanceof Heading1WithMdContent}
      <svelte:component this={c.component} content={c.content} />
  {/if}

  {#if c instanceof ParagraphWithMdContent}
      <svelte:component this={c.component} content={c.content} />
  {/if}

{/each}