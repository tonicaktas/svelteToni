<script>

	// These values are bound to properties of the video
	let time = 0;
	let duration;
	let paused = true;
    export let src; 

	let showControls = true;
	let showControlsTimeout;

	// Used to track time of last mouse down event
	let lastMouseDown;

	function handleMove(e) {
		// Make the controls visible, but fade out after
		// 2.5 seconds of inactivity
		clearTimeout(showControlsTimeout);
		showControlsTimeout = setTimeout(() => showControls = false, 2500);
		showControls = true;

		if (!duration) return; // video not loaded yet
		if (e.type !== 'touchmove' && !(e.buttons & 1)) return; // mouse not down

		const clientX = e.type === 'touchmove' ? e.touches[0].clientX : e.clientX;
		const { left, right } = this.getBoundingClientRect();
		time = duration * (clientX - left) / (right - left);
	}

	// we can't rely on the built-in click event, because it fires
	// after a drag — we have to listen for clicks ourselves
	function handleMousedown(e) {
		lastMouseDown = new Date();
	}

	function handleMouseup(e) {
		if (new Date() - lastMouseDown < 300) {
			if (paused) e.target.play();
			else e.target.pause();
		}
	}

</script>

<video
    poster="{src}"
    src="{src}/webm_product_high"
    on:mousemove={handleMove}
    on:touchmove|preventDefault={handleMove}
    on:mousedown={handleMousedown}
    on:mouseup={handleMouseup}
    bind:currentTime={time}
    bind:duration
    bind:paused>
    <track kind="captions">
</video>

<style type="text/scss">
    video {
        width: 100%;
        margin: 10px;
		position: relative;
		z-index: 0;

        @media screen and (min-width: 1024px) {	
            width: 40%;
            margin:5px;	
        }
    }
</style>