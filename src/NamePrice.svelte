<script>
    export let name;
	export let brand;
    export let price;
	export let discount;
    export let ordprice;
</script>

<div class="name-price-holder">
    <div class="name-holder">
        <span>{brand}</span>
        <h1>{name}</h1>
    </div>
    <div class="price-holder">
        <div class="discount-holder">
            <p>{discount}</p>
            <p>{ordprice}</p>
        </div>       
        <p>{price}</p>
    </div>
</div>

<style type="text/scss">
    .name-price-holder {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        margin: 10px auto 15px;
        .name-holder {
            display: flex;
            flex-direction: column;

            span {
                color: #000;
                font-size: 1.2rem;
                letter-spacing: 1px;

                @media screen and (min-width: 767px) {		
                    color: #adadad;
                    font-size: .75rem;
                }
            }

            h1 {
                color: #adadad;
                font-weight: 300;
                font-size: 1rem;
                line-height: 80%;
                margin: 10px 0;
                letter-spacing: 1px;

                @media screen and (min-width: 767px) {		                  
                    color: #474646;
                    font-size: 1.25rem;
                }
            }
        }
        .price-holder {
            display: flex;
            flex-direction: column;
            .discount-holder {
                display: flex;
                p {
                    font-size: .75rem;
                    margin: 0 5px 0 0;

                    @media screen and (min-width: 767px) {		                  
                        //font-size: rem;
                    }
                    &:first-child {
                        color: #af0303;
                    }
                    &:last-child {
                        color: #000;
                        text-decoration: line-through;
                    }
                }
            }

            p {
                color: #af0303;
                font-size: 1.25rem;
                margin: 5px 0;
                font-weight: 300;

                @media screen and (min-width: 767px) {		                  
                    font-size: 1.5rem;
                }
            }
        }
    }
</style>