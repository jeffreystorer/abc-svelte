<script>
    import { v4 as uuidv4} from 'uuid';
    export let data;
    let values = [null];
    if ('values' in data.players ) values = JSON.parse(JSON.stringify(data.players.values));
    values.shift();
    export let tds = values;
    const playerCount = tds.length;
    export let colorCount;
    switch (true) {
        case playerCount < 5:
        colorCount = playerCount;
        break;
        case playerCount < 8:
        colorCount = 4;
        break;
        case playerCount >= 8:
        colorCount = 8;
        default:
        break;
    }
</script>
  
{#if ('values' in data.players === false)}
    <h2>Next Friday&apos;s list<br />will be available on Monday</h2>
{:else}
    <ol>
        {#each tds as td, i (uuidv4())}
        <li class={i < colorCount ? 'in' : 'out'}>
            {td[1]} {td[2]}
        </li>
        {/each}
    </ol>
{/if}



<style>
    h2 {
        margin: 0 auto;
        padding: 0;
        text-align: center;
    }

    ol {
        margin: 0 auto;
        text-align: left;
        width: fit-content;
    }

    ol li {
        font-size: var(--step-4);
        font-weight: 700;
    }
    
    .in {
    color: green;
    }
        
    .out {
    color: red;
    }

		
</style>
