<script lang="ts">
	import { fade } from 'svelte/transition';
	import TextField from './TextField.svelte';
	import RadioOptions from './RadioOptions.svelte';
	import Attendees from './Attendees.svelte';
	import { goto } from '$app/navigation';

	let coming: 'coming' | 'no-coming' | undefined = undefined;
	let hasName = false;
	let form: HTMLFormElement;

	let attendeeCount = 1;
	let reception = true;

	const MAX_ATTENDEES = 11;

	function nameChange(event: Event) {
		const target = event.target as HTMLInputElement;
		hasName = target.value.length > 0;
		event.preventDefault();
		event.stopPropagation();
	}

	function onAttendeeCountChange(event: Event) {
		const target = event.target as HTMLInputElement;
		const attendeeCountString = target.value;
		attendeeCount = parseInt(attendeeCountString) || 1;
	}

	function onSubmit(event: Event) {
		event.preventDefault();

		const myForm = event.target as HTMLFormElement;
		const formData = new FormData(myForm);

		fetch('/', {
			method: 'POST',
			headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
			body: new URLSearchParams(formData as any).toString()
		})
			.then((response) => {
				if (!response.ok) {
					throw new Error('Form submission failed');
				}
				console.log('Form successfully submitted');
				goto('/thanks');
			})
			.catch((error) => alert(error));
	}
</script>

<div id="rsvp-form">
	<form name="rsvp" method="POST" bind:this={form} data-netlify="true" on:submit={onSubmit}>
		<input type="hidden" name="form-name" value="rsvp" />

		<TextField label="full name" name="name-1" required on:change={nameChange} />
		<TextField label="email" name="email" type="email" required />

		<RadioOptions
			bind:selected={coming}
			options={{ coming: 'I am coming', 'not-coming': "I can't make it" }}
			name="coming"
			required
		/>

		{#if coming === 'coming'}
			<div id="coming" in:fade>
				<TextField
					min={1}
					max={MAX_ATTENDEES}
					name="count"
					label="number of guests"
					type="number"
					required
					on:change={onAttendeeCountChange}
				/>

				<Attendees count={attendeeCount} />

				<h2>I will attend:</h2>
				<div class="field-grid">
					<input type="checkbox" checked name="ceremony" id="ceremony" />
					<label for="ceremony">Ceremony <span class="time">11am</span></label>
					<input type="checkbox" name="reception" id="reception" bind:checked={reception} />
					<label for="reception">Reception <span class="time">2pm</span></label>
					<input type="checkbox" checked name="ceilidh" id="ceilidh" />
					<label for="ceilidh">Cèilidh (dance) <span class="time">7pm</span></label>
				</div>
			</div>
		{:else}
			<input type="hidden" name="count" value="0" />
			<Attendees count={0} />
			<input type="hidden" name="ceremony" value="false" />
			<input type="hidden" name="reception" value="false" />
			<input type="hidden" name="ceilidh" value="false" />
		{/if}

		{#if coming === 'coming' && reception}
			<textarea name="dietary" id="dietary" placeholder="Dietary requirements (gluten-free, dairy-free, vegan, nut free)" in:fade />
		{:else}
			<input type="hidden" name="dietary" value="" />
		{/if}
		<textarea name="comments" id="comments" placeholder="Other comments" />

		<input type="submit" />
	</form>
</div>

<style>
	#rsvp-form {
		max-width: 80%;
		min-width: 300px;
		padding: 1.5rem 30px 1.5rem 30px;
		margin: 2rem auto;
		background-color: #ffffff;
		border-radius: 5px;
		box-shadow: 0 15px 35px rgba(50, 50, 93, 0.1), 0 5px 15px rgba(0, 0, 0, 0.07);
	}

	form {
		display: flex;
		position: relative;
		flex-direction: column;
		align-items: stretch;
		width: 100%;
		font-size: 1.3rem;
	}

	input[type='checkbox'] {
		width: 1.2rem;
		height: 1.2rem;
	}

	.field-grid {
		display: grid;
		align-items: center;
		grid-template-columns: auto 1fr;
		grid-gap: 0.5rem;
		padding-left: 0.5rem;
	}

	input[type='submit'] {
		color: white;
		background-color: rgb(26, 148, 188);
		padding: 0.5rem 1rem;
		border-radius: 2rem;
		border: none;
		margin-top: 1rem;
	}

	input[type='submit']:hover {
		background-color: rgba(22, 122, 155);
	}

	textarea {
		padding: 0.5rem 1rem;
		border-radius: 0.2rem;
		border: 1px solid var(--color-border);
		margin: 1rem 0;
		font-family: var(--font-body);
		font-size: 1rem;
		resize: vertical;
	}

  span.time {
    font-size: 0.9rem;
    color: var(--color-text-secondary);
  }
</style>
