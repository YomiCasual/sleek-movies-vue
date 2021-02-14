<template>
	<header>
		<router-link to="/" class="flex-item">
			<h1>Sleek<span>Movies</span></h1>
		</router-link>
    <div @click="changeTheme" class="icon">
		<svg v-if="!darkMode"
		xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
		<path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z" />
		</svg>
		<svg v-else 
		xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
		<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
		</svg>
	</div>
	</header>

	<main class="background" :class="[darkMode ? 'darkMode' : 'lightMode']" >
		<router-view />
	</main>
</template>


<script>
export default {
  data() {
    return {
      darkMode: false
    }
  },
  methods: {
    changeTheme: function() {
      this.darkMode = !this.darkMode
    }
  }
}
</script>

<style lang="scss">
* {
	margin: 0;
	box-sizing: border-box;
  font-family: "Fira Sans", sans-serif!important;
}

body {
	padding: 0;
}

a {
	text-decoration: none;
}

header {
	display: flex;
	align-items: center;
	justify-content: center;
	padding: 10px;
	background-color: #2c3d4e;
	box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.3);
	position: fixed;
	top: 0;
	z-index: 600;
	width: 100%;

	.flex-item {
		width: 80%;
		text-align: center;
	}

	h1 {
		color: white;

		span {
			color: #42b883;
		}
	}

	.icon {
		font-size: 20px;
		width: 30px;
		color: white;
		cursor: pointer;
		transition: 0.5s all ease
	}

}
.darkMode {
  background-color: #040e1a!important;
  transition: 0.5s all ease;
  /* min-height: 100%; */

  input {
			&[type='text'] {
				color: white!important;
				background-color: #496583!important;
				border: 1px solid #35495e!important;
				margin-bottom: 1rem;
			}

			&::placeholder {
				color: rgba(201, 197, 197, 0.747)!important
			}
	}
  .movie-content {
	color: rgb(224, 223, 223)!important;
	background-color: #243547;
	border-radius: 0 0 8px 8px!important;
  }
  .movie-detail {
	p {
		color: white!important
	}

	.section {
		h3 {
			color: #319e6d!important
		}
	}
  }
}

.lightMode {
  background-color: white;
  transition: 0.5s all ease;
}

.background {
  height: 100%;
  width: 100%;
}

  
</style>
