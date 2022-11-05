<template>
    <div class="lists" >
        <h4>{{post.description}}</h4>
        <p>{{post.value}}</p>
        <div style="display:flex; align-items: center;">
            <p>{{post.date}}</p>
            <span class="material-symbols-outlined icon">delete</span>
        </div>
    </div>
</template>

<script>
export default {
    props:['post'],
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