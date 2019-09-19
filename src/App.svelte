<script>

	import { Router, Link, Route } from "svelte-routing";
	import Mar1 from "./animaciones/Mar1.svelte";
	import Inicio from "./Inicio.svelte";

	export let url = "";
</script>

<style>
	h1 {
		color: purple;
	}
</style>


<Router url="{url}">

	<header class="cabecera-principal">
		
		<div class="logotipo">
			<h4>
				CCD - ADC
			</h4>
		</div>

		<nav>
			<ul>
				<li>
					<Link to="/">Inicio</Link>
				</li>
				<li>
					<Link to="/mar1">Mar 1</Link>
				</li>
			</ul>
		</nav>

	</header>

	<main>

		<Route path="mar1" component="{Mar1}" />
		<Route path="/" component="{Inicio}" />

	</main>

	<footer>
		Pie
	</footer>

</Router>