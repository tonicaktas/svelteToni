<script>
    import Icon from 'svelte-icons-pack/Icon.svelte';
    import FaSolidShoppingBag from "svelte-icons-pack/fa/FaSolidShoppingBag";
    import FaHeart from "svelte-icons-pack/fa/FaHeart";
</script>

<div class="btn-cart-holder">
    <button class="add-to-cart">
        <p>Lägg till</p>
        <div class="bag-icon" >
            <Icon color="white" src={FaSolidShoppingBag} />
        </div>
    </button>
    <button class="heart-holder">
        <Icon src={FaHeart} />
    </button>
</div>

<style type="text/scss">
    .btn-cart-holder {
        display: inline-block;
        flex-direction: row;
        justify-content: space-between;
        width: 50%;
        height: 40px;
        
        @media screen and (min-width: 767px) {		
            display: flex;
            width: 100%;
        }

        .add-to-cart {
            color: #fff;
            background: pink;
            border: 1px solid pink;
            width: 100%;
            position: relative;
            transition: .3s;
            height: 100%;
            

            @media screen and (min-width: 767px) {		
                width: 75%;
            }

            &:hover {
                color: pink;
                background: white;
                cursor: pointer;
            }

            p {
                margin: 0;
                font-size: calc((1.3 - 1) * 1vw + .5rem);
                letter-spacing: 1px;
            }

            .bag-icon {
                color: #fff;
                position: absolute;
                right: 10px;
                top: 7px;
            }

        }
        .heart-holder {
            width: 20%;
            background: #fff;
            display: none;

            @media screen and (min-width: 767px) {		
                display: block;
                height: 40px;
            }
        }
    }
</style>