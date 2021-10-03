<script>
    export let classname;
    export let group;
    export let style;
</script>

<dic class="breadcrumps">
    <p>{classname}</p> - <p>{group}</p> - <p>{style}</p>
</dic>

<style type="text/scss">
    .breadcrumps {
        display: flex;
        flex-direction: row;
        align-items: center;
        
        @media screen and (min-width: 767px) {
			display: none;
		}
        p {
            font-size: calc((1.2 - 1) * .8vw + .5rem);
            letter-spacing: 1px;
            margin-bottom: 10px;
            text-transform: capitalize;
            text-decoration: underline;
            margin: 0 5px;

            &:first-child {
                margin-left: 0;
            }
        }     
    }
</style>