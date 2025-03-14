<script>
	import QRCode from '@castlenine/svelte-qrcode';
	let value = $state('');
	let fixValue = $state('');
	let downloadUrl = $state('');

	const handleDownloadUrlGenerated = (url = '') => {
		downloadUrl = url;
	};
	const handleReset = () => {
		fixValue = '';
		value = '';
		downloadUrl = '';
	};
	const handleGenerate = () => {
		fixValue = value;
	};
</script>

<div class="mx-auto flex max-w-[1000px] flex-col gap-6 py-24">
	<div class="flex flex-col gap-6">
		<input type="text" bind:value class="input w-full" placeholder="Link here" />
		<div class="grid grid-cols-3 gap-6">
			<button onclick={handleGenerate} class="btn btn-primary"> Generate </button>
			<button onclick={handleReset} class="btn btn-warning">Reset</button>

			{#if downloadUrl}
				<a
					href={downloadUrl}
					download={`${Date.now()}.png`}
					target="_blank"
					class="btn btn-secondary"
				>
					Download QR Code
				</a>
			{/if}
		</div>
	</div>
	<div>
		{#if fixValue}
			<QRCode
				data={fixValue}
				downloadUrlFileFormat="png"
				dispatchDownloadUrl
				on:downloadUrlGenerated={(event) => handleDownloadUrlGenerated(event.detail.url)}
				logoPath={'/sesabyldc.png'}
				logoSize={10}
				size={1000}
			/>
		{/if}
	</div>
</div>
