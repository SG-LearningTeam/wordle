<script lang="ts">
    import { gameWritable } from "../ts/game";
    export let keyboardPress: (key: string) => void;

    const keyboard = [
        ["q", "w", "e", "r", "t", "y", "u", "i", "o", "p"],
        ["a", "s", "d", "f", "g", "h", "j", "k", "l"],
        ["enter", "z", "x", "c", "v", "b", "n", "m", "backspace"],
    ];

    export let keyboardDiv: HTMLDivElement;
</script>

<div class="keyboard" bind:this={keyboardDiv}>
    {#key $gameWritable}
        {#each keyboard as keyboardRow}
            <div class="keyboardRow" style="--columns: {keyboardRow.length}">
                {#each keyboardRow as key}
                    {#if key.length !== 1}
                        {#if key === "backspace"}
                            <button class="specialKey" on:click={() => keyboardPress(key)}
                                ><svg width="40" height="30" fill="currentColor" viewBox="0 0 16 16">
                                    <path
                                        d="M5.83 5.146a.5.5 0 0 0 0 .708L7.975 8l-2.147 2.146a.5.5 0 0 0 .707.708l2.147-2.147 2.146 2.147a.5.5 0 0 0 .707-.708L9.39 8l2.146-2.146a.5.5 0 0 0-.707-.708L8.683 7.293 6.536 5.146a.5.5 0 0 0-.707 0z"
                                    />
                                    <path
                                        d="M13.683 1a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2h-7.08a2 2 0 0 1-1.519-.698L.241 8.65a1 1 0 0 1 0-1.302L5.084 1.7A2 2 0 0 1 6.603 1h7.08zm-7.08 1a1 1 0 0 0-.76.35L1 8l4.844 5.65a1 1 0 0 0 .759.35h7.08a1 1 0 0 0 1-1V3a1 1 0 0 0-1-1h-7.08z"
                                    />
                                </svg></button
                            >
                        {:else}
                            <button class="specialKey" on:click={() => keyboardPress(key)}>{key}</button>
                        {/if}
                    {:else}
                        <button class="key" style="background-color:{$gameWritable.getColor($gameWritable.keyboardColors[key], true)}" on:click={() => keyboardPress(key)}>{key.toUpperCase()}</button>
                    {/if}
                {/each}
            </div>
        {/each}
    {/key}
</div>

<style>
    .keyboard {
        display: flex;
        flex-direction: column;
        align-items: center;
        position: fixed;
        bottom: 12px;
    }

    .keyboardRow {
        display: flex;
        justify-content: center;
        gap: 3px;
    }

    .key {
        width: min(9.4vw, 60px);
        height: min(9.4vh, 75px);
        border-radius: 4px;
        border-color: black;
        background-color: white;
        transition: background-color 0.3s;
    }

    :global(body.darkMode) .key {
        background-color: lightgrey;
    }

    .specialKey {
        width: 80px;
        height: min(9.4vh, 75px);
        border-radius: 4px;
        border-color: black;
        background-color: lightgrey;
        font-weight: bold;
        transition: background-color 0.3s;
    }

    :global(body.darkMode) .specialKey {
        background-color: grey;
    }
</style>
