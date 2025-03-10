<script lang="ts">
	import { onMount } from 'svelte';
	import PlajHome from '$lib/assets/previews/plajhome.png';

	let initTextRef = $state<HTMLParagraphElement>();
	let mainDiv = $state<HTMLDivElement>();
	let section = $state<HTMLDivElement>();

	const firstWord = 'hi';
	let initText = $state(firstWord);

	function type({
		text,
		startFrom = '',
		delay = 50,
		wait = 200,
		onFinish
	}: {
		text: string;
		startFrom?: string;
		delay?: number;
		wait?: number;
		onFinish?: () => void;
	}) {
		let currentChar = 0;
		initText = startFrom;
		const loop = setInterval(() => {
			initText = initText + text[currentChar];
			currentChar++;
			if (initText.length === startFrom.length + text.length) {
				clearInterval(loop);
				if (onFinish) setTimeout(onFinish, wait);
			}
		}, delay);
	}

	function clear({
		letters,
		delay = 50,
		wait = 200,
		onFinish
	}: {
		letters?: number;
		delay?: number;
		wait?: number;
		onFinish?: () => void;
	}) {
		const toDelete = letters ? letters : initText.length;
		let count = 0;

		const loop = setInterval(() => {
			initText = initText.slice(0, -1);
			count++;

			if (count === toDelete) {
				clearInterval(loop);
				if (onFinish) setTimeout(onFinish, wait);
			}
		}, delay);
	}

	function loop() {
		type({
			text: 'code frontend',
			startFrom: "hi, i'm seb, i ",
			wait: 1000,
			onFinish: () => {
				clear({
					letters: 8,
					onFinish: () => {
						type({
							text: 'backend',
							startFrom: "hi, i'm seb, i code ",
							wait: 1000,
							onFinish: () => {
								clear({
									letters: 12,
									onFinish: () => {
										type({
											text: 'design ui',
											startFrom: "hi, i'm seb, i ",
											wait: 1000,
											onFinish: () => {
												clear({
													letters: 2,
													onFinish: () => {
														type({
															text: 'ux',
															startFrom: "hi, i'm seb, i design ",
															wait: 1000,
															onFinish: () => {
																clear({
																	letters: 10,
																	onFinish: loop
																});
															}
														});
													}
												});
											}
										});
									}
								});
							}
						});
					}
				});
			}
		});
	}

	function animateText() {
		type({
			text: ", i'm seb",
			wait: 1000,
			startFrom: firstWord,
			onFinish: () => {
				type({
					text: ', i ',
					startFrom: "hi, i'm seb",
					wait: 0,
					onFinish: () => {
						loop();
						mainDiv?.classList.remove('translate-y-[calc(calc(50dvh-10rem))]');
						section?.classList.remove('opacity-0');
						setTimeout(() => {
							document.body.style.overflow = 'auto';
						}, 5000);
					}
				});
			}
		});
	}

	onMount(() => {
		if (initTextRef) {
			initTextRef.classList.remove('hidden');
			initTextRef.animate(
				[
					{ transform: `translateY(${window.innerHeight}px)`, display: 'block' },
					{ transform: 'translateY(0)', display: 'block' }
				],
				{
					duration: 1000,
					easing: 'cubic-bezier(0.215, 0.61, 0.355, 1)',
					fill: 'forwards'
				}
			).onfinish = animateText;
		}
	});
</script>

<div
	bind:this={mainDiv}
	class="relative w-full translate-y-[calc(calc(50dvh-10rem))] overflow-hidden transition-transform duration-700"
>
	<div class="mt-20 h-[96px] w-3/4">
		<div class="relative w-fit">
			<p
				class="hidden text-2xl after:absolute after:bottom-[-15px] after:ml-[1px] after:h-[32px] after:w-[3px] after:-translate-y-1/2 after:bg-neutral-700"
				bind:this={initTextRef}
			>
				{initText}
			</p>
		</div>
	</div>
	<div
		class="rounded-lg border border-neutral-700 bg-neutral-800 p-4 opacity-0 transition-opacity duration-700"
		bind:this={section}
	>
		<h2 class="mb-2 text-2xl">Projects</h2>
		<div class="flex flex-wrap">
			<div class="w-full max-w-80 rounded-lg border border-neutral-600 bg-neutral-900 p-4">
				<h2 class="text-xl font-medium">PlajHome</h2>
				<p class="mb-2">
					Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed non risus. Suspendisse lectus
					tortor, dignissim sit amet, adipiscing nec, ultricies sed, dolor.
				</p>
				<img src={PlajHome} alt="screenshot of plajhome" class="rounded-md" />
			</div>
		</div>
	</div>
</div>
