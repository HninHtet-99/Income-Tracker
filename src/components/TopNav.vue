<template>
    <div>
        <div class="title">
            <input type="date" v-model="incomeDate">
            <input type="text" placeholder="Income Description" v-model="incomeDes">
            <input type="number" placeholder="Income Value" v-model="incomeValue" @keyup="save">
            <button class="btn" @click="add">Add</button>
        </div>
        <div v-for="post in posts" :key="post.id">
            <SinglePost :post="post"></SinglePost>
        </div>
        
    </div>

</template>

<script>
import SinglePost from './SinglePost'
export default {
  components: { SinglePost },
    data(){
        return{
            incomeDes:'',
            incomeValue: '',
            incomeDate: '',
            posts:[]
        }
    },
    mounted(){
        fetch("http://localhost:3000/posts")
        .then((response)=>{
            return response.json();
        })
        .then((datas)=>{
            this.posts = datas;
        })
        .catch((err)=>{
            console.log(err.message);
        })
    },
    methods:{
        save(e){
            if (e.keyCode == 13) {
                this.add();
            }
        },
        add(){
            if (this.incomeDes===''&& this.incomeValue==='') {
                    alert('please check again!')
                }
                else{
                    console.log(this.incomeDes,this.incomeValue,this.incomeDate);
                }
        }
    }

}
</script>

<style>
.title{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
input{
    border: none;
    padding: 10px;
}
.btn{
    margin-left: 2px;
    padding: 5px 10px;
    border: 1px solid rgb(141, 226, 56);
    border-radius: 10px;
    background-color: #fff;
}
.btn:hover{
    background-color: rgb(141, 226, 56);
}
.lists{
    background-color: #f5f5f5;
    max-width: 600px;
    margin: 10px auto;
    padding: 10px 20px;
    border-radius: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>