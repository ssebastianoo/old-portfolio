<script lang="ts">
	import { ChevronsDown } from '@lucide/svelte';
</script>

<div class="flex min-h-[calc(100dvh-3.5rem-124px)] flex-col items-center">
	<div class="flex w-full max-w-md flex-col gap-3">
		<div class="flex justify-end">
			<div
				class="w-fit max-w-80 animate-[from-bottom_0.7s_cubic-bezier(0.18,1.12,0.7,0.96)_forwards_4s] rounded-tl-2xl rounded-tr-2xl rounded-bl-2xl bg-sky-900 px-2 py-1 opacity-0"
			>
				<p>who are you?</p>
			</div>
		</div>
		<div
			class="w-fit max-w-80 animate-[from-bottom_0.7s_cubic-bezier(0.18,1.12,0.7,0.96)_forwards_4.5s] rounded-tl-2xl rounded-tr-2xl rounded-br-2xl bg-neutral-700 px-2 py-1 opacity-0"
		>
			<p>
				i'm a computer science student from italy, i'm a software development nerd, i like to create
				full stack apps to make my life easier
			</p>
		</div>
		<div class="flex justify-end">
			<div
				class="w-fit max-w-80 animate-[from-bottom_0.7s_cubic-bezier(0.18,1.12,0.7,0.96)_forwards_5s] rounded-tl-2xl rounded-tr-2xl rounded-bl-2xl bg-sky-900 px-2 py-1 opacity-0"
			>
				<p>so what can you do?</p>
			</div>
		</div>
		<div
			class="w-fit max-w-80 animate-[from-bottom_0.7s_cubic-bezier(0.18,1.12,0.7,0.96)_forwards_5.5s] rounded-tl-2xl rounded-tr-2xl rounded-br-2xl bg-neutral-700 px-2 py-1 opacity-0"
		>
			<p>
				my main focus is on frontend development, i have much experience with javascript and
				typescript frameworks
			</p>
		</div>
		<div
			class="w-fit max-w-80 animate-[from-bottom_0.7s_cubic-bezier(0.18,1.12,0.7,0.96)_forwards_6s] rounded-tl-2xl rounded-tr-2xl rounded-br-2xl bg-neutral-700 px-2 py-1 opacity-0"
		>
			<p>
				but i also worked in backend development managing databases, apis and linux infrastructures
			</p>
		</div>
		<div class="flex justify-end">
			<div
				class="w-fit max-w-80 animate-[from-bottom_0.7s_cubic-bezier(0.18,1.12,0.7,0.96)_forwards_6.5s] rounded-tl-2xl rounded-tr-2xl rounded-bl-2xl bg-sky-900 px-2 py-1 opacity-0"
			>
				<p>can you show me something?</p>
			</div>
		</div>
	</div>
	<div
		class="flex h-[calc(100%-1.75rem)] flex-1 animate-[appear_1s_cubic-bezier(0.18,1.12,0.7,0.96)_forwards_7s] flex-col items-center justify-center gap-1 opacity-0"
	>
		<p>projects</p>
		<ChevronsDown />
	</div>
</div>
