<script>
	// Props for the SVG element
	export let svgId = 'mySvg'; // ID of the SVG element to download
	export let fileName = 'download.svg'; // Default file name
	export let buttonText = 'Download SVG';
	export let buttonClass = 'download-button';

	// Function to download the SVG
	const downloadSVG = () => {
		const svgElement = document.getElementById(svgId);

		if (!svgElement) {
			alert('SVG element not found!');
			return;
		}

		// Clone the SVG to avoid modifying the original
		const clonedSvg = svgElement.cloneNode(true);

		// Get SVG markup as string
		const svgData = new XMLSerializer().serializeToString(clonedSvg);

		// Create a Blob with the SVG data
		const blob = new Blob([svgData], { type: 'image/svg+xml' });

		// Create a download link
		const url = URL.createObjectURL(blob);
		const link = document.createElement('a');
		link.href = url;
		link.download = fileName;
		document.body.appendChild(link);

		// Trigger download
		link.click();

		// Clean up
		URL.revokeObjectURL(url);
		document.body.removeChild(link);
	};
</script>

<button class={buttonClass} on:click={downloadSVG}>
	{buttonText}
</button>

<style>
	.download-button {
		background-color: #4a90e2;
		color: white;
		border: none;
		border-radius: 4px;
		padding: 10px 15px;
		font-size: 16px;
		cursor: pointer;
		transition: background-color 0.2s;
	}

	.download-button:hover {
		background-color: #3a7bc8;
	}

	.download-button:active {
		background-color: #2a6cb8;
	}
</style>
