<template>
  <main class="container">
      <p>Sei nella pagina numero {{currentPage}}</p>
      <p>In totale ci sono {{lastPage}}</p>
    <div class="row">
        <div class="col-sm-6" v-for="post in posts" :key="post.id">
            <div class="card">
                <div class="card-body">
                    <h5 class="card-title">{{post.title}}</h5>
                    <p class="card-text">{{post.content}}</p>
                    <a href="#" class="btn btn-primary">Dettagli</a>
                </div>
            </div>
        </div>
    </div>

    <nav aria-label="Page navigation example">
        <ul class="pagination">
            <li class="page-item"><button class="page-link" href="#" 
            @click="getPosts(currentPage - 1)">Previous</button></li>
            <li class="page-item"><a class="page-link" href="#">1</a></li>
            <li class="page-item"><a class="page-link" href="#">2</a></li>
            <li class="page-item"><a class="page-link" href="#">3</a></li>
            <li class="page-item"><button class="page-link" href="#" 
            @click="getPosts(currentPage + 1)">Next</button></li>
        </ul>
    </nav>
  </main>
</template>


<script>
export default {
  name: "Main",
  data() {
      return {
          chiamataApi: 'http://127.0.0.1:8000/api/posts',
          posts: [],
          currentPage: 1, 
          lastPage:null

      }
  },
  created(){
      this.getPosts();
  },
  methods: {
      getPosts(){
           axios.get(this.chiamataApi)
                .then(response => {
                    this.posts = response.data.results.data;
                    // console.log(response.data.results);
                    this.currentPage = response.data.results.current_page;
                    this.lastPage = response.data.results.last_page;

                })
      }
  }
}
</script>

<style lang="scss" scoped>
</style>