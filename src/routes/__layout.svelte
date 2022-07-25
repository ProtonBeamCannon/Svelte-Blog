<script context="module">  
  /** @type {import('@sveltejs/kit').Load} */
  export const load = async ({fetch}) => {
    const resourceUrl = `/pages.json`;
    const res = await fetch(resourceUrl);
  
    if (res.ok) {
      const {pages} = await res.json()
      return {
        props: {pages},
      };
    }
  
    return {
      status: res.status,
      error: new Error(`Could not load url`)
    };
  }
</script>

<script>
import '../app.css' 
import Nav from '$lib/nav.svelte';
export let pages;

import {onMount} from 'svelte'
import {themeChange} from 'theme-change'
onMount(async () => {
  themeChange(false)
})
</script>
<Nav {pages}/>
<main class="container max-w-xl mx-auto px-4">
  <slot />

</main>
