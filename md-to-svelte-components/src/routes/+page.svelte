<script lang="ts">
    import Main from '$lib/components/Main.svelte';
  
    let markdown = '';
  </script>
  
  <textarea rows="10" cols="50" bind:value={markdown}>

  </textarea>
  
  <Main {markdown}/>
  