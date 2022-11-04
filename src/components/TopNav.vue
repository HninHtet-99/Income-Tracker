<template>
    <div>
        <div class="title">
            <input type="date" v-model="incomeDate">
            <input type="text" placeholder="Income Description" v-model="incomeDes">
            <input type="number" placeholder="Income Value" v-model="incomeValue" @keyup="save">
            
            <button class="btn" type="submit">Add</button>
        </div>
        <div class="lists">
            <h3>{{incomeDes}}</h3>
            <p>{{incomeValue}}</p>
            <p>{{incomeDate}}</p>
        </div>
    </div>

</template>

<script>
export default {
    data(){
        return{
            incomeDes:'',
            incomeValue: '',
            incomeDate: ''
        }
    },
    methods:{
        save(e){
            if (e.keyCode == 13) {
                if (this.incomeDate==' ' && this.incomeDes===''&& this.incomeValue==='') {
                    alert('please check again!')
                }
                else{
                    console.log(this.incomeDes,this.incomeValue,this.incomeDate);
                }
                
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