<script>
                let wishList = [
                  { text: "Write my first post", status: true },
                  { text: "Upload the post to the blog", status: false },
                  { text: "Publish the post at Facebook", status: false }
                ];
</script>

{#each wishList as wish, index}
	<span class:checked={wish.status}>{wish.text}</span>
	<input bind:checked={wish.status} type="checkbox">
	<br/>
{/each} 


<style>
 .checked {
   text-decoration: line-through;
 }
</style> 