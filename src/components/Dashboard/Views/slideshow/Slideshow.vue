<template>
    <div class='row'>
      <div class='col-md-12'>
        <div class='card'>
          <router-link to="/slideshow/add">
            <v-btn class="pull-right"><i class="ti-plus"></i> Slideshow</v-btn>
          </router-link>
          <v-client-table :data="tableData" :columns="columns" name="dt" :options="options">
          </v-client-table>
        </div>
        </div>
      </div>
    </div>
</template>
<script>
import Firebase from 'firebase'
import Content from './content.vue'
// import Price from './Price.vue'
export default {
  data () {
    return {
      columns: ['type', 'create', 'title', 'Action'],
      tableData: [],
      options: {
        templates: {
          Action: Content,
          headings: {
            create: 'Created at',
            type: 'Type',
            title: 'Title'
          }
        }
      }
    }
  },
  mounted: function () {
    this.definedata()
    this.$session.remove('edit')
  },
  methods: {
    definedata () {
      let _this = this
      Firebase.database().ref('slideshow').on('value', function (snapshot) {
        let dt = snapshot.val()
        _this.tableData = []
        for (let key in dt) {
          let obj = dt[key]
          obj.key = key
          obj.create = _this.$moment(obj.created_at).format('DD MMM YYYY HH:mm')
          _this.tableData.push(obj)
        }
      })
    }
  }
}
</script>
<style>

</style>
