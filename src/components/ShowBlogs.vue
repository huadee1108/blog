<template>
    <div v-theme:column="'wide'" id="show-blogs">
        <h1>博客总览</h1>
        <input type="text" v-model="search" placeholder="搜索">
        <div v-for="blog in filteredBlogs" class="single-blog">
            <h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
            <article>
                {{blog.body | snippet}}
            </article>
        </div>
    </div>
</template>

<script>
    export default {
        name: "show-blogs",
        data(){
            return{
                blogs:[],
                search:''
            }
        },
        created(){
            this.$http.get('http://jsonplaceholder.typicode.com/posts'
            )
                .then(function (response) {
                    //console.log(response)
                    this.blogs = response.data.slice(0,10);
                    console.log(this.blogs);
                })

        },
        computed:{
            filteredBlogs:function () {
                return this.blogs.filter((blog) =>{
                    return blog.title.match(this.search);
                })
            }
        }
    }
</script>

<style scoped>
#show-blogs{
    max-width: 800px;
    margin: 0 auto;
}
.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
</style>
