<template>
	<div>
    <v-btn @click="edit"><i class="ti-pencil"></i></v-btn>
    <v-btn @click="del"><i class="ti-trash"></i></v-btn>
	</div>
</template>
<script>
import Firebase from 'firebase'
export default{
  props: ['data'],
  methods: {
    edit () {
      console.log(this.data)
      this.$session.set('edit', this.data)
      this.$router.push('setting/accounts/edit')
    },
    del () {
      let dele = confirm('Yakin ingin menghapus?')
      if (dele) {
        Firebase.database().ref('accounts').child(this.data.key).remove()
        this.$router.push('/setting')
      }
    }
  }
}
</script>
