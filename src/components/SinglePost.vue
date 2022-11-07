<template>
    <div class="lists" >
        <h4 style="width:160px">{{post.description}}</h4>
        <p style="width:60px;text-align:end">$ {{post.value}}</p>
        <div style="display:flex; align-items: center;">
            <p>{{post.date}}</p>
            <span class="material-symbols-outlined icon" @click="deletePost">delete</span>
        </div>
    </div>
</template>

<script>
export default {
    props:['post'],
    methods:{
        deletePost(){
            fetch('http://localhost:3000/posts/'+this.post.id,{method:"DELETE"})
            .then(()=>{
                this.$emit("delete",this.post.id);
            })
            .catch((err)=>{
                console.log(err.message);
            })
        }
    }
}
</script>

<style>

.icon{
    font-size: 20px;
    margin-left: 20px;
    color: red;
    cursor: pointer;
}
</style>