<script>
	import Button from "./Button.svelte";
	import Input from "./Input.svelte";
	import { evaluate } from "mathjs";

	let input = "";
	let trapInput = [];
	let buttons = [
		"1",
		"2",
		"3",
		"+",
		"4",
		"5",
		"6",
		"-",
		"7",
		"8",
		"9",
		"&divide;",
		"AC",
		"0",
		"=",
		"&times;",
	];
	let symbols = ["+", "-", "&divide;", "&times"];
	function doTheMath(event) {
		const clickedButton = event.detail.value;
		let mathString = "";
		let solution = "";
		switch (clickedButton.toLowerCase()) {
			case "=":
				mathString = trapInput.join("");
				try {
					solution = evaluate(mathString);
				} catch (error) {
					input += "<br/>Bad math Error";
					trapInput = [];
				}
				
				input = solution;
				trapInput = [solution];
				break;
			case "ac":
				input = "";
				trapInput = [];
				break;
			case "&divide;":
				if (trapInput.length !== 0) {
					input += clickedButton;
					trapInput = [...trapInput, "/"];
				} else {
					input = "";
				}
				break;
			case "&times;":
				if (trapInput.length !== 0) {
					input += clickedButton;
					trapInput = [...trapInput, "*"];
				} else {
					input = "";
				}
				break;

			default:
				input += clickedButton;
				trapInput = [...trapInput, clickedButton];
				break;
		}
		console.log(trapInput);
		console.log(mathString);
		console.log(solution);
	}
</script>

<!-- This example requires Tailwind CSS v2.0+ -->
<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
	<!-- We've used 3xl here, but feel free to try other max-widths based on your needs -->
	<div class="max-w-3xl mx-auto">
		<!-- Content goes here -->

		<!-- This example requires Tailwind CSS v2.0+ -->
		<div class="bg-white overflow-hidden shadow rounded-lg">
			<div class="px-4 py-5 sm:px-6">
				<Input {input} />
			</div>
			<div class="bg-gray-50 px-4 py-5 sm:p-6">
				<div class="grid grid-cols-4 gap-2">
					{#each buttons as button}
						<Button
							buttonText={button}
							on:buttonClicked={doTheMath} />
					{/each}
				</div>
			</div>
		</div>
	</div>
</div>
