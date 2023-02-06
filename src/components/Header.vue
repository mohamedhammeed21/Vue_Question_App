<template>
    <ul>
        <li>
            <strong>Quiz App</strong>
        </li>
        <li>Counter {{correct}}/{{total}}</li>
        <hr>
    </ul>
   
</template>

<script>
export default {
    name:'Header',
    props:{
        correct:Number,
        total:Number
    }
}
</script>

<style  scoped>
    ul{
        list-style: none;
         text-align: left;
         padding: 0;
         margin: 10px ;

    }
    li{
        display: inline;
        text-align: left;
        margin-right: 20px;
    }
</style>