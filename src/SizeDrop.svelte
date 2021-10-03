<script>
    export let size;
    export let soldout;   
</script>

<select class="size-select">
    <option selected>Välj storlek</option>
    {#each size as siz}
        Storlek:<option value={siz.Name}> {siz.Name}</option>
    {/each} 
    {#each soldout as SoldOutSizes}
        Storlek:<option disabled value={SoldOutSizes.Name}> {SoldOutSizes.Name}</option>
    {/each} 
</select>

<style type="text/scss">
    .size-select {
        width: calc(50% - 10px);
        font-size: .75rem;
        letter-spacing: 1px;
        display: inline-block;
        height: 40px;
        background: #fff;

        @media screen and (min-width: 767px) {		
            width: 100%;
            padding: 10px;
        }

        &:focus {
            outline: none;
        }
    }
</style>

    
    