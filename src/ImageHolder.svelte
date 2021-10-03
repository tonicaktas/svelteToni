<script>
	import Video from './Video.svelte'
    import Icon from 'svelte-icons-pack/Icon.svelte';
    import IoArrowBackOutline from "svelte-icons-pack/io/IoArrowBackOutline";
    import IoArrowForward from "svelte-icons-pack/io/IoArrowForward";
    import FaHeart from "svelte-icons-pack/fa/FaHeart";
    import { onMount } from 'svelte';

    export let res
    
    const props = {
        color : "#000",
        size: "2rem",
    }

    const propsheart = {
        color : "#000",
        size: "1.5rem",
    }
    
    let imgHolder;
    let rootElement;
    let prevBtn;
    let nextBtn;

    onMount(() => {
        const imgDiv = rootElement.querySelector('.img-holder');
        const firstImg = imgDiv.firstElementChild;
        const secImg = firstImg.nextElementSibling;
        const lastImg = imgDiv.lastElementChild;
        const nextToLast = lastImg.previousElementSibling;

        console.log(secImg);

        function isInViewport(el) {
            const rect = el.getBoundingClientRect();
            return (
                rect.top >= 0 &&
                rect.left >= 0 &&
                rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
                rect.right <= (window.innerWidth || document.documentElement.clientWidth)
            );
        }

        if(isInViewport(firstImg)) {
            prevBtn.style.display = "none";
        }

        nextBtn.addEventListener('click', function () {
            isInViewport(secImg) ?
            "" : 
            prevBtn.style.display = "block";
          
            isInViewport(nextToLast) ?
            nextBtn.style.display = "none" : 
            nextBtn.style.display = "block";
          
            let scrollWidth = imgDiv.firstElementChild.clientWidth + 22;
            imgDiv.scrollBy({ left: scrollWidth, behavior: 'smooth' });

        }, {
            passive: true
        });

        prevBtn.addEventListener('click', function () {
            isInViewport(secImg) ?
            prevBtn.style.display = "none" : 
            prevBtn.style.display = "block";

            isInViewport(nextToLast) ?
            "" : 
            nextBtn.style.display = "block";
          
            let scrollWidth = imgDiv.firstElementChild.clientWidth + 22;
            imgDiv.scrollBy({ left: - scrollWidth, behavior: 'smooth' });            
        }, {
            passive: true
        });
    })

</script>

    <div class="holder" bind:this={rootElement}>
        <button class="prev-btn" bind:this={prevBtn} >
            <Icon {...props} src={IoArrowBackOutline} />
        </button>
        <div class="img-holder" height="75" bind:this="{imgHolder}">
            {#each res as {type, src }, i}
            
                {#if type === "img" && i < 3}
                    <img src={src} alt="Nelly"/>
                    {:else if type === "video"}	
                    <Video src={src} />
                {/if} 
            {/each}
        </div>
        <button class="next-btn" bind:this={nextBtn}>
            <Icon {...props} src={IoArrowForward} />
        </button>
        <button class="heart-mobile" >
            <Icon {...propsheart}  src={FaHeart} />
        </button>
    </div>

<style type="text/scss">
	.holder {
		position: relative;
		top: 0;
		width: 100%;

        @media screen and (min-width: 1024px) {		
            width: 65%;
        }

		button {
			position: absolute;
			bottom: 10px;
			border-radius: 50%;
            z-index: 3;
            width: 50px;
            height: 50px;

			&.prev-btn {
				left: 10px;
                padding-left: 10px;
			}

			&.next-btn {
				right: 10px;
                padding-right: 10px;
			}

            &.heart-mobile {
                bottom: 75px;
                right: 10px;
                padding-top: 10px;
                margin: 0;
            }

			@media screen and (min-width: 1024px) {		
				display: none;
			}
		}

		.img-holder {
			display: flex;
			flex-direction: row;
			overflow: scroll;
			height: 70vh;
			
			@media screen and (min-width: 1024px) {
				flex-wrap: wrap;
				flex-direction: row;
				justify-content: center;
				width: 100%;
				position: relative;
				height: 100%;
			}	
			
			img {
				margin: 10px;
                width: calc(100% - 20px);
				max-width: 100%;

				@media screen and (min-width: 1024px) {		
					width: 40%;
					margin:5px;
				}
			}
		}
	}

</style>