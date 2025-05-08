<script lang="ts">
    export let content = "";

    $: heading1 = parseHeading1(content)

    function parseHeading1(content:string) : string {
        return content
    }

</script>

<h1>{heading1}</h1>