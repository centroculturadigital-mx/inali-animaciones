<script>

	import { Router, Link, Route } from "svelte-routing";
	import Mar1 from "./animaciones/Mar1.svelte";
	import Mar2 from "./animaciones/Mar2.svelte";
	import Mar3 from "./animaciones/Mar3.svelte";
	import Mar4 from "./animaciones/Mar4.svelte";
	import Mar5 from "./animaciones/Mar5.svelte";
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
				<li>
					<Link to="/mar2">Mar 2</Link>
				</li>
				<li>
					<Link to="/mar3">Mar 3</Link>
				</li>
				<li>
					<Link to="/mar4">Mar 4</Link>
				</li>
				<li>
					<Link to="/mar5">Mar 5</Link>
				</li>
			</ul>
		</nav>

	</header>

	<main>

		<Route path="/mar1" component="{Mar1}" />
		<Route path="/mar2" component="{Mar2}" />
		<Route path="/mar3" component="{Mar3}" />
		<Route path="/mar4" component="{Mar4}" />
		<Route path="/mar5" component="{Mar5}" />
		<Route path="/" component="{Inicio}" />

	</main>

	<footer>
		Pie
	</footer>

</Router>