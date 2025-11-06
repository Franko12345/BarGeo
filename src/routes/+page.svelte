<script>
	import Br from "$lib/components/Br.svelte";
</script>

<div class="app">
	<header class="header">
		<h1>🍸 Bar Geo</h1>
		<p>Descubra o sabor do Brasil, um estado de cada vez.</p>
	</header>

	<main class="content">
		<Br />
	</main>

	<footer class="footer">
		<p>Feito com 💙 por amantes dos bares e da cultura brasileira.</p>
		<p>Trabalho escolar por Franco Valois, Samuel Batista, Maria Luiza e Luiz Guilherme</p>
	</footer>
</div>

<style>
	:global(html, body) {
		margin: 0;
		padding: 0;
		background: radial-gradient(circle at 50% 20%, #0a0f18 0%, #030509 100%);
		color: #e0e0e0;
		font-family: 'Poppins', sans-serif;
		height: 100%;
		overflow-x: hidden;
	}

	.app {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: space-between;
		min-height: 100vh;
		padding: 2rem;
		box-sizing: border-box;
		text-align: center;
	}

	.header {
		margin-bottom: 2rem;
		animation: fadeInDown 0.8s ease;
	}

	.header h1 {
		font-size: 3rem;
		background: linear-gradient(135deg, #0099ff, #00ffaa);
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		text-shadow: 0 0 12px rgba(0, 204, 255, 0.3);
		font-weight: 700;
		margin: 0;
	}

	.header p {
		color: #aaa;
		font-size: 1.1rem;
		margin-top: 0.5rem;
		letter-spacing: 0.5px;
	}

	.content {
		flex: 1;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		max-width: 900px;
		border-radius: 20px;
		padding: 2rem;
		background: rgba(15, 25, 35, 0.6);
		box-shadow: 0 0 30px rgba(0, 0, 0, 0.5);
		backdrop-filter: blur(10px);
		transition: all 0.4s ease;
	}

	.content:hover {
		transform: scale(1.01);
		box-shadow: 0 0 40px rgba(0, 140, 255, 0.25);
	}

	.footer {
		margin-top: 2rem;
		font-size: 0.9rem;
		color: #666;
	}

	@keyframes fadeInDown {
		from {
			opacity: 0;
			transform: translateY(-20px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}
</style>
