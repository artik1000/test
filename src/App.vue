<template>
  <form action="#" method="post" id="filter" onsubmit="return false">
    <FormIn ref="form1"/>
    <FormIn ref="form2"/>
    <FormIn ref="form3"/>
    <div><input type="submit" @click="PostRequest()" value="send"/></div>
  </form>
</template>

<script>
import FormIn from './components/FormIn.vue'

export default {
  name: 'App',
  components: {
      FormIn
  },
    data () {
      return{
      }
    },
  methods:{
      PostRequest (){
          this.$refs.form1.PostVid();
          this.$refs.form2.PostVid();
          this.$refs.form3.PostVid();
      }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
