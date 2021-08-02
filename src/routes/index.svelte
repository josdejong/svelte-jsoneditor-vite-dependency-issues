<script>
  import { JSONEditor } from 'svelte-jsoneditor'

  let json = {
    greeting: 'hello world!'
  }
</script>

<JSONEditor bind:json />
