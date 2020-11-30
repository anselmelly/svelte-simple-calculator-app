<script>
    import { createEventDispatcher } from "svelte";
    export let buttonText;

    const dispatch = createEventDispatcher();

    function buttonClicked(value) {
        dispatch("buttonClicked", {
            value: value,
        });
    }
</script>

<button
on:click="{buttonClicked(buttonText)}"
    class="
    inline-flex 
    items-center px-5 py-5 
    border 
    border-transparent 
    text-2xl
    lg:text-3xl font-bold 
    rounded-none text-indigo-700 
    bg-indigo-100 
    hover:bg-indigo-200 
    focus:outline-none 
    focus:ring-2 focus:ring-offset-2 
    focus:ring-indigo-500">{@html buttonText}</button>
