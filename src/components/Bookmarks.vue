<template>
  <div>
    <h1>Bookmarks</h1>
    <div v-if="bookmarks.length === 0">No Bookmarks</div>
    <ul v-else>
      <li v-for="bookmark in bookmarks" :key="bookmark._id">
        {{ bookmark.url }}
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data(){
      return {
        bookmarks: []
      }
    },
    async mounted() {
      this.fetchBookmarks();
    },
    methods: {
      fetchBookmarks: async function () {
        let apiResponse = await this.$http.get("http://localhost:8000/api/bookmarks");
        if (apiResponse.status === 200) {
          this.bookmarks = apiResponse.data.bookmarks;
        }
      }
    }
  }
</script>