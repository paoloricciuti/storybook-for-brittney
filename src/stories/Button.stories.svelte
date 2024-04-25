<script lang="ts" context="module">
	import type { Meta } from '@storybook/svelte';
	export const meta: Meta = {
		title: 'Button',
		argTypes: {
			size: {
				control: 'select',
				options: ['small', 'medium', 'large']
			}
		}
	};
</script>

<script lang="ts">
	import { Story, Template } from '@storybook/addon-svelte-csf';
	import { within, expect, fn, userEvent } from '@storybook/test';
	import Button from './Button.svelte';
</script>

<Template id="main" let:args>
	<Button {...args} on:click={args.click} />
</Template>

<Story
	name="Primary"
	template="main"
	args={{
		primary: false,
		backgroundColor: '#bada55',
		size: 'small',
		label: 'Cool',
		click: fn() // <-- this create a mock function that you can expect on (args, how many time is called etc)
	}}
	play={async ({ canvasElement, args, step }) => {
		const canvas = within(canvasElement); // <-- this allow you to query by role, label etc (like testing library)
		const button = await canvas.findByRole('button');
		await step("button it's in the document", () => {
			// <-- with step you perform steps in the interaction
			expect(button).toBeInTheDocument();
		});
		await step('clicking it send a click event', async () => {
			await userEvent.click(button); // <-- perform user actions with userEvent from @storybook/test
			expect(args.click).toHaveBeenCalled();
		});
	}}
></Story>
