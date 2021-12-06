<script>
    export let name;
    export let primaryType;
    export let secondaryType = false;
    export let imageUrl;
    let colorTypeLookup = { 
        "normal" : "#a8a878",
        "fire" : "#f08030",
        "water" : "#6890f0",
        "grass" : "#78c850",
        "electric" : "#f8d030",
        "ice" : "#98d8d8",
        "fighting" : "#c03028",
        "poison" : "#a040a0",
        "ground" : "#e0c068",
        "flying" : "#a890f0",
        "psychic" : "#f85888",
        "bug" : "#a8b820",
        "rock" : "#b8a038",
        "ghost" : "#705898",
        "dark" : "#705848",
        "dragon" : "#7038f8",
        "steel" : "#b8b8d0",
        "fairy" : "#f0b6bc"
    };
</script>

<main style="background-color: {colorTypeLookup[primaryType]}">
    <div class="name">
        <p>{name}</p>
    </div>
    <div class="type">
        <p class="primary" style="background-color: {colorTypeLookup[primaryType]}">{primaryType}</p>
        {#if secondaryType}
            <p class="secondary" style="background-color: {colorTypeLookup[secondaryType]}">{secondaryType}</p>
        {/if}
    </div>
    <img src={imageUrl} alt="Image of {name}">
</main>

<style>
    main {
        margin: 20px;
        color: White;
        display: inline-flex;
        
        border-top-left-radius: 5px;
        border-top-right-radius: 20px;
        border-bottom-right-radius: 5px;
        border-bottom-left-radius: 5px;

        border-width: 3px;
        border-color: white;

        width:230px;
        height: 100px;
        
        justify-content: space-between;
        overflow: hidden;
        position: relative;
    }

    p {
        margin: 0;
        padding: 5px;
        text-transform: capitalize;
    }

    .primary {
        background-color: turquoise;
    }

    .secondary {
        background-color: blue;
    }

    .type {
        border-top-right-radius: 5px;
        overflow: hidden;
        display: flex;

        position: absolute;
        left: 0;
        bottom: 0;
    }

    .name {
        background-color: rgb(80, 79, 79);
        border-bottom-right-radius: 5px;
        min-width: 100px;

        position: absolute;
        left: 0;
        top: 0;
    }

    img {
        width: 100px;
        height: 100px;

        margin-left: auto;
    }
</style>