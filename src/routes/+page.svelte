<script>
    import { onMount } from "svelte";


    let input;

    let numbers = [];

    onMount(() => {
        input.focus();
    })
    
    function handleKeyDown(ev) {
        if (ev.key == "Enter") {
            numbers = [...numbers, new Number(input.value)];

            input.value = "";
        }

        else if (ev.key == "Escape") {
            numbers = [];
            input.value = "";
        }
    }
    
    function getGCD(arr) {
        const gcd = (a, b) => {
            if (a == 0) return b;

            return gcd(b % a, a);
        }

        let result = arr[0]
        arr.forEach((n, idx) => {
            if (idx == 0) return;

            result = gcd(n, result);

            if (result == 1) {
                return 1;
            }
        })

        return result;
    }

    $: gcd = getGCD(numbers) || 0;
</script>

<svelte:head>
    <title>
        Greatest Common Factor
    </title>
</svelte:head>

<svelte:window 
    on:keydown={handleKeyDown}
/>

<main>
    <div class="container">
        GCF([
        <span class="important">
            {#each numbers as number}
                {number},&NonBreakingSpace;
            {/each}
            <input type="text" bind:this={input}>
        </span>
        ]) = <span class="important">{gcd}</span>
    </div>
</main>

<style>
    main {
        height: 100vh;
        
        display: grid;
        place-items: center;
    }

    div.container {
        font-size: 50px;
        color: gray;
    }

    div.container input {
        font-family: var(--apple-font);
        font-size: 50px;
        width: 70px;
    }

    .important {
        color: black;
        font-family: var(--apple-font);
    }
</style>