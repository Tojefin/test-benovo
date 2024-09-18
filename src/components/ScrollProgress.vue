<script>
const body = document.querySelector('body');
const observer = new ResizeObserver(function() {
	updateProgress()
});
observer.observe(body)

window.onscroll = function () { updateProgress() }

function updateProgress() {
	var winScroll = document.body.scrollTop || document.documentElement.scrollTop
	var height = document.documentElement.scrollHeight - document.documentElement.clientHeight
	if (!height) {
		document.getElementById("box").style.opacity = "0"
	} else {
		document.getElementById("box").style.opacity = "1"
	}
	var scrolled = (winScroll / height) * 100
	document.getElementById("bar").style.width = scrolled + "%"
	console.log(height,winScroll,scrolled)
}
</script>

<template>
	<div class="progress-container" id="box">
		<div class="progress-bar" id="bar"></div>
	</div>
</template>

<style scoped>
.progress-container {
	width: 100vw;
	height: 4px;
	background: #ccc;
	position: fixed;
	top: 0;
	left: 0;
	z-index: 10;
}

.progress-bar {
	height: 4px;
	background: #63bffc;
	width: 0%;
}
</style>