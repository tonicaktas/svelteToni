<script>
    export let description;
    let descArrray = description.split("<br />");
</script>

<div class="beskrivning-holder">
    <h2>Beskrivning</h2>
    <ul>
        {#each descArrray as listItem}
            <li>{listItem}</li>
        {/each}
    </ul>
</div>

<style type="text/scss">
    .beskrivning-holder {
        margin-top: 25px;
        h2 {
            color: #000;
            font-weight: 300;
            font-size: 1rem;
            line-height: 80%;
            margin: 10px 0;
            letter-spacing: 1px;
            text-transform: uppercase;
        }

        ul {
            padding-left: 17px;
            li {
                font-size: .75rem;
                letter-spacing: 1px;
                margin-bottom: 10px;
            }
        }
    }
</style>