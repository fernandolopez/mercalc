<script>
	import { resolve } from '$app/paths';
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>
<ul>
    <li><a class="link" href={resolve('/lineal')}>Por metro</a></li>
    <li><a class="link" href={resolve('/mass')}>Por peso</a></li>
    <li><a class="link" href={resolve('/volume')}>Por litro</a></li>
</ul>