<template>
    <div>
        <div class="title">
            <input type="date" v-model="incomeDate">
            <input type="text" placeholder="Income Description" v-model="incomeDes">
            <input type="number" placeholder="Income Value" v-model="incomeValue" @keyup="save">
            <button class="btn" @click="add">Add</button>
        </div>
        <div v-for="post in posts" :key="post.id">
            <SinglePost :post="post" @delete="deletePostList"></SinglePost>
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
            posts:[],
            totalIncome: 0
        }
    },
    methods:{
        /* delete income */
        deletePostList(id){
            this.posts = this.posts.filter((post)=>{
                return post.id != id;
            })
            this.total;
        },
        /* add income */
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
                    fetch("http://localhost:3000/posts",{
                        method : "POST",
                        headers:{
                            "Content-Type":"application/json"
                        },
                        body:JSON.stringify(
                            {
                                description: this.incomeDes,
                                value: this.incomeValue,
                                date: this.incomeDate
                            }
                        )
                    })
                    .then((response)=>{
                        return response.json();
                    })
                    .then((post)=>{
                        this.posts.push(post);
                        this.total;
                    })
                    .catch((err)=>{
                        console.log(err.message);
                    })
                }
                this.incomeDate = '';
                this.incomeDes = '';
                this.incomeValue = ''
                
        }

    },
    mounted(){
        /* fetch data */
        fetch("http://localhost:3000/posts")
        .then((response)=>{
            return response.json();
        })
        .then((datas)=>{
            this.posts = datas;
            this.total;
        })
        .catch((err)=>{
            console.log(err.message);
        })
        
    },
    /* calculate total income */
    computed:{
        total(){
          this.totalIncome = this.posts.reduce((preValue,curValue)=>{
            return preValue+curValue.value;
           },0)
           this.$emit("showTotal",this.totalIncome)
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
    border: 1px solid rgb(187, 194, 90);
    border-radius: 10px;
    background-color: #fff;
}
.btn:hover{
    background-color: rgb(217, 225, 96);
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