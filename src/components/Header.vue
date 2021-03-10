<template>
    <div class="m-content">
        head
        <h3>欢迎来到Markerhub博客</h3>
        <div class="block"><el-avatar :size="50" :src="user.avatar"></el-avatar></div>
        <div>{{user.username}}</div>
        <template>
            <div class="maction">
                <span><el-link :underline="false" href="/blogs">主页</el-link></span>
                <el-divider direction="vertical" href="/blog/add"></el-divider>
                <span><el-link :underline="false" type="success">发表文章</el-link></span>
                <el-divider direction="vertical"></el-divider>
                <span v-show="!hasLogin"><el-link :underline="false" type="primary" href="/login">登录</el-link></span>

                <span v-show="hasLogin"><el-link :underline="false" type="danger" @click="logout">退出</el-link></span>

            </div>
        </template>
            </div>
            </template>

            <script>

        export default {
            name: "Header",
            data(){
                return{
                    user:{
                        username:'请先登录',
                        avatar:'https://cube.elemecdn.com/9/c2/f0ee8a3c7c9638a54940382568c9dpng.png'
                    },
                    hasLogin:false
                }

            },
            methods:{
                logout(){
                    const _this=this
                    _this.$axios.get("/logout",{
                        headers:{
                            "Authorization":localStorage.getItem("token")
                        }
                    }).then(res=>{
                        _this.$store.commit("REMOVE_INFO")
                        _this.$router.push("/login")
                    })
                }
            },created() {
                if(this.$store.getters.getUser.username){
                    this.user.username=this.$store.getters.getUser.username
                    this.user.avatar=this.$store.getters.getUser.avatar
                    this.hasLogin=true
                }
            }
        }

</script>

<style scoped>
.m-content{
    max-width: 960px;
    margin: 0 auto;
    text-align: center;
}
    .maction{
        margin: 10px auto;
    }
</style>