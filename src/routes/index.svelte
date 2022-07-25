<script context="module">  
  /** @type {import('@sveltejs/kit').Load} */
  export const load = async ({fetch}) => {
    const resourceUrl = `/posts.json`;
    const res = await fetch(resourceUrl);
  
    if (res.ok) {
      const {posts} = await res.json()
      return {
        props: {posts},
      };
    }
  
    return {
      status: res.status,
      error: new Error(`Could not load url`)
    };
  }
</script>
<script>
  export let posts 

</script>

<svelte:head>
  <!-- head content -->
  <title>SK Blog | Welcome</title>
</svelte:head>

<h1 class="text-4xl mb-10 font-extrabold">
  SK Blog
</h1>

{#each posts as {title,slug,excerpt,coverImage,tags}}
   <!-- content here -->
   <div class="card text-center shadow-2xl mb-20">
    <figure class="pd-10 pt-10">
      <img class="rounded-xl" src={coverImage.url} alt={`Cover image for ${title}`}>
    </figure>
    <div class="card-body">
      <h2 class="title">
        {title}
      </h2>
        <p>{excerpt}</p>
        <div class="flex justify-center mt-5 space-x-2">
          {#each tags as tag}
             <!-- content here -->
             <span class="badge badge-primary">{tag}</span>
          {/each}
        </div>
      <div class="justify-center card-actions">
        <a href={`/posts/${slug}`} class="btn btn-outline btn-primary">
        Read &rAarr;
        </a>
      </div>
    </div>
   </div>
{:else}
   <!-- empty list -->
{/each}