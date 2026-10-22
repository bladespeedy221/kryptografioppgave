<script>
	let value = '';
	let key = 0;
	let vigenereKey = '';
	let method = 'caesar';

	function caesarCipher(match) {
		const charCode = match.toLowerCase().charCodeAt(0);
		const code = ((charCode - 97 + key) % 26) + 97;
		return String.fromCharCode(code);
	}

	function vigenereEncrypt(text, keyword) {
		if (!keyword) return text;

		let result = '';
		let keyIndex = 0;

		for (let i = 0; i < text.length; i++) {
			const char = text[i];

			if (/[a-z]/i.test(char)) {
				const shift =
					keyword[keyIndex % keyword.length].toLowerCase().charCodeAt(0) - 97;

				const code =
					((char.toLowerCase().charCodeAt(0) - 97 + shift) % 26) + 97;

				result += String.fromCharCode(code);
				keyIndex++;
			} else {
				result += char;n
				``
			}
		}

		return result;
	}

	$: output =
		method === 'caesar'
			? value.replace(/[a-z]/gi, caesarCipher)
			: vigenereEncrypt(value, vigenereKey);
</script>

<style>
	:global(body) {
		font-family: Arial, sans-serif;
		background-color: #f4f6f8;
		margin: 0;
		padding: 40px;
		display: flex;
		justify-content: center;
	}

	form {
		background: white;
		padding: 2rem;
		border-radius: 12px;
		box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
		width: 100%;
		max-width: 500px;
		display: flex;
		flex-direction: column;
		gap: 1rem;
	}

	label {
		font-weight: bold;
		color: #333;
	}

	input,
	select {
		padding: 0.75rem;
		border: 1px solid #ccc;
		border-radius: 8px;
		font-size: 1rem;
	}

	input:focus,
	select:focus {
		outline: none;
		border-color: #2563eb;
		box-shadow: 0 0 5px rgba(37, 99, 235, 0.3);
	}

	h1 {
		background: #2563eb;
		color: white;
		padding: 1rem;
		border-radius: 8px;
		word-wrap: break-word;
		font-size: 1.2rem;
		text-align: center;
		margin-top: 1rem;
	}

	.title {
		text-align: center;
		color: #2563eb;
		margin-bottom: 1rem;
	}
</style>
``

<form on:submit|preventDefault>
	<label>Tekst:</label>
	<input bind:value />

	<label>Metode:</label>
	<select bind:value={method}>
		<option value="caesar">Caesar</option>
		<option value="vigenere">Vigenère</option>
	</select>

	{#if method === 'caesar'}
		<label>Nøkkel (0-25):</label>
		<input
			type="number"
			bind:value={key}
			min="0"
			max="25"
			step="1"
		/>
	{/if}

	{#if method === 'vigenere'}
		<label>Vigenère-nøkkel:</label>
		<input bind:value={vigenereKey} />
	{/if}

	<h1>{output}</h1>
</form>