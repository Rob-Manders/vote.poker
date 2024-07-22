<script>
    import votersstore from "./store/voters";
    import roomstore from "./store/room";

    export let value = 0;
    $: selected = $votersstore.my_vote === value;

    function placeVote(value) {
        if (!$roomstore.votes_revealed) {
            if (selected) {
                votersstore.placeVote("");
            } else {
                votersstore.placeVote(value);
            }
        }
    }
</script>

<div class="voting-option">
    <div class="card { (selected ? 'selected' : '') + ' ' + (!$roomstore.votes_revealed ? 'selectable' : '')}" on:click={ () => placeVote(value) }>
        { value }
    </div>
</div>


<style>
    .voting-option {
        position: relative;
        height: 90px;
        display: flex;
    }

    .card {
        background-color: var(--card-colour);
        height: 100px;
        width: 100px;
        max-width: 100px;
        border-top-left-radius: 10px;
        border-top-right-radius: 10px;
        padding: 10px;
        margin: 0 3px -1px 3px;
        font-size: 4em;
        font-weight: bold;
        flex: 10%;
        align-self: flex-end;
        transition: 150ms ease-in-out;
        box-shadow: 0 -5px 15px -10px rgba(0, 0, 0, 0.75);
    }

    .voting-option::after {
        position: absolute;
        content: '';
        left: -3px;
        right: -3px;
        bottom: -10px;
        height: 30px;
        background: linear-gradient(0deg, var(--background-colour) 0%, var(--background-colour) 35%, rgba(0, 0, 0, 0) 100%);
    }

    div.selectable:hover {
        cursor: pointer;
    }

    div.selectable:hover, div.selected {
        background: var(--card-colour-active);
        /*color: white;*/
        height: 115px;
    }

    @media (prefers-color-scheme: dark) {
        .card {
            background-color: var(--card-colour_dark);
        }

        .voting-option::after {
            background: linear-gradient(0deg, var(--background-colour_dark) 0%, var(--background-colour_dark) 35%, rgba(0, 0, 0, 0) 100%);
        }

        div.selectable:hover, div.selected {
            background-color: var(--card-active-colour_dark);
        }
    }
</style>
