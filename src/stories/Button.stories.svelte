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
	import Button from './Button.svelte';
</script>

<Template id="main" let:args>
	<Button {...args} />
</Template>

<Story
	name="Primary"
	template="main"
	args={{
		primary: false,
		backgroundColor: '#bada55',
		size: 'small',
		label: 'Cool'
	}}
></Story>
