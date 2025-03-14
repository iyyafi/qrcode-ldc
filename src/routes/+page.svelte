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

<input type="text" bind:value />
<button onclick={handleGenerate}>Generate</button>
<button onclick={handleReset}>Reset</button>

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

{#if downloadUrl}
	<a href={downloadUrl} download="QR-code-filename.png" target="_blank">Download QR Code</a>
{/if}
