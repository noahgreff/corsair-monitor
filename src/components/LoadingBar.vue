<template>
    <div id="loading-bar"></div>
</template>

<style lang="scss" scoped>
    
    @import './src/assets/styles/variables.scss';
    
	#loading-bar {
		position: absolute;
		z-index: 1000;
		bottom: 0;
        height: 5px;
		animation: load 1500ms ease-out infinite;
        background: $theme;
    }

    @keyframes load {
		0% {
			width: 0;
			left: 0;
		}
		40% {
			width: 75%;
			left: 0;
		}
		80% {
			width: 0;
			left: 100%;
		}
		100% {
			width: 0;
			left: 100%;
		}
    }
    
</style>