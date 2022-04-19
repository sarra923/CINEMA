<template>

  <div id="nav">
    <router-link to="/">Accueil</router-link> |
    <router-link to="/recherche">Recherche</router-link>
  </div>
  <router-view/>
</template>

<script>
export default {
	name: 'App',
	methods: {
		getList(){
			this.axios.get(api).then((response) => {
				console.log(response.data)
			})
		}
	}
}
</script>



<style lang ="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #FFFFFF;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #FFFFFF;
}

#nav a.router-link-exact-active {
  color: deeppink;
}
</style>
