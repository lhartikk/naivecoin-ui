<template>
  <div>
    <table>
      <thead>
      <tr>
        <th>#</th>
        <th>hash</th>
        <th>Transactions</th>
        <th>Timestamp</th>
      </tr>
      </thead>

      <tbody>
      <tr v-for="block in sortBlocks(blocks)">
        <td>{{ block.index }}</td>
        <td><router-link :to="{ name: 'Block', params: { id: block.hash }}">{{ block.hash }}</router-link></td>
        <td>{{ block.data.length }}</td>
        <td>{{ block.timestamp}}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'FrontPage',
    data() {
      return {
        blocks: []
      }
    },
    created() {
      this.getBlocks();
    },
    methods: {
      getBlocks: function () {
        this.$http.get('/api/blocks')
          .then((resp) => {
            this.blocks = resp.data;
          })
      },
      sortBlocks : function(blocks) {
        return _(blocks)
          .sortBy('index')
          .reverse()
          .value();
      }
    }
  }
</script>


<style scoped>

</style>
