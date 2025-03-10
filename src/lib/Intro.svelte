<script lang="ts">
	import { onMount } from 'svelte';

	let initTextRef = $state<HTMLParagraphElement>();
	let mainDiv = $state<HTMLDivElement>();

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
						setTimeout(() => {
							document.body.style.overflow = 'auto';
						}, 500);
					}
				});
			}
		});
	}

	onMount(() => {
		// mainDiv?.classList.remove('translate-y-[calc(calc(50dvh-10rem))]');
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
	class="relative flex translate-y-[calc(calc(50dvh-10rem))] justify-center overflow-hidden transition-transform duration-700"
>
	<div class="mt-10 mb-5 h-[64px]">
		<div class="relative w-fit">
			<p
				class="hidden text-2xl after:absolute after:bottom-[-15px] after:ml-[1px] after:h-[32px] after:w-[3px] after:-translate-y-1/2 after:bg-neutral-700"
				bind:this={initTextRef}
			>
				{initText}
			</p>
		</div>
	</div>
</div>
