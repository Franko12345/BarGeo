<script>
	let { showModal = $bindable(), header, children } = $props();
	let dialog = $state(); // HTMLDialogElement

	// abre/fecha o dialog quando showModal mudar
	$effect(() => {
		if (showModal) {
			try { dialog.showModal(); } catch (e) { /* fallback */ }
			dialog.focus();
		} else {
			if (dialog && dialog.open) dialog.close();
		}
	});

	// fechar via ESC / cancel
	function handleCancel(e) {
		e.preventDefault();
		showModal = false;
	}

	// clique no backdrop fecha
	function backdropClose(e) {
		if (e.target === dialog) dialog.close();
	}
</script>

<!-- svelte-ignore a11y_click_events_have_key_events, a11y_no_noninteractive_element_interactions -->
<dialog
	bind:this={dialog}
	on:close={() => (showModal = false)}
	on:cancel={handleCancel}
	on:click={backdropClose}
	class="modal"
	aria-modal="true"
>
	<div class="panel" role="dialog" aria-label="Modal">
		<header class="panel-header">
			<div class="title">
				{@render header?.()}
			</div>
			<button class="close" aria-label="Fechar" on:click={() => dialog.close()}>
				<svg width="16" height="16" viewBox="0 0 24 24" fill="none" aria-hidden>
					<path d="M6 6L18 18M6 18L18 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
				</svg>
			</button>
		</header>

		<section class="panel-body">
			{@render children?.()}
		</section>

		<footer class="panel-footer">
			<button class="btn" on:click={() => dialog.close()}>Fechar</button>
		</footer>
	</div>
</dialog>

<style>
	:root{
		--bg-0: #05060a;
		--bg-1: #071025;
		--panel: linear-gradient(180deg, rgba(10,16,28,0.96), rgba(4,8,14,0.98));
		--accent: #1f6fb6;
		--muted: #9fb0c8;
		--radius: 14px;
		--shadow: 0 30px 60px rgba(3,8,20,0.7);
	}

	/* backdrop moderno: escuro + blur */
	dialog::backdrop{
		background:
			radial-gradient(1200px 800px at 30% 10%, rgba(30,40,60,0.30), transparent 10%),
			linear-gradient(180deg, rgba(1,4,10,0.64), rgba(1,2,6,0.8));
		backdrop-filter: blur(6px) saturate(120%);
		-webkit-backdrop-filter: blur(6px) saturate(120%);
	}

	/* base do dialog - fixamos centro com transform */
	dialog.modal{
		border: none;
		padding: 0;
		background: transparent; /* o painel interno tem o fundo */
		position: fixed;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		z-index: 9999;
		width: 94vw;
		max-width: 920px;
		outline: none;
	}

	/* painel interno arredondado e sombreado */
	.panel{
		background: var(--panel);
		border-radius: var(--radius);
		box-shadow: var(--shadow);
		overflow: hidden;
		color: #eaf6ff;
		display: flex;
		flex-direction: column;
		max-height: 80vh;
		width: 100%;
	}

	/* animação de pop */
	dialog[open] .panel{
		animation: pop 1000ms cubic-bezier(.2,.9,.2,1);
	}
	@keyframes pop {
		from { transform: translateY(6px) scale(.995); opacity: 0; }
		to   { transform: translateY(0) scale(1); opacity: 0.6; }
	}

	.panel-header{
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 1rem;
		padding: 1rem 1.25rem;
		border-bottom: 1px solid rgba(255,255,255,0.03);
		background: linear-gradient(180deg, rgba(255,255,255,0.02), transparent);
	}

	.title h2{ margin:0; font-size:1.05rem; color:#eaf6ff; }
	.title small{ display:block; color:var(--muted); font-size:0.85rem; margin-top:0.18rem; }

	.close{
		appearance: none;
		border: none;
		background: transparent;
		color: var(--muted);
		padding: 0.35rem;
		border-radius: 8px;
		cursor: pointer;
		transition: background 160ms, color 160ms, transform 160ms;
	}
	.close:hover{ background: rgba(255,255,255,0.02); color: var(--accent); transform: translateY(-1px); }

	.panel-body{
		padding: 1rem 1.25rem;
		overflow: auto;
		color: #dbeafe;
	}

	.panel-footer{
		padding: 0.8rem 1.25rem;
		border-top: 1px solid rgba(255,255,255,0.03);
		display:flex;
		justify-content: flex-end;
		gap: 0.5rem;
		background: linear-gradient(180deg, transparent, rgba(255,255,255,0.01));
	}

	.btn{
		background: linear-gradient(90deg, rgba(30,111,184,0.14), rgba(30,111,184,0.06));
		border: 1px solid rgba(30,111,184,0.12);
		color: #dff2ff;
		padding: 0.5rem 0.9rem;
		border-radius: 10px;
		cursor: pointer;
		font-weight: 600;
		transition: transform 160ms, box-shadow 160ms;
	}
	.btn:hover{ transform: translateY(-2px); box-shadow: 0 8px 24px rgba(18,46,78,0.28); }

	/* mobile tweaks */
	@media (max-width:520px){
		dialog.modal{ width: 96vw; max-width: 96vw; top: 52%; transform: translate(-50%, -52%); }
		.panel{ border-radius: 12px; }
		.panel-body{ padding: 0.9rem; }
		.panel-header, .panel-footer { padding: 0.9rem; }
	}
</style>
