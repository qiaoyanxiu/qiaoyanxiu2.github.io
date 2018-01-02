<template>
    <div class="app">
            <h1>商品信息</h1>
            <table>
                <thead>
                <tr>
                    <td>商品信息</td>
                    <td>单价</td>
                    <td>数量</td>
                    <td>添加到购物车</td>
                </tr>
                </thead>
                <tbody>
                <tr v-for="(user,index) in users">
                    <td>{{user.name}}</td>
                    <td>{{user.price}}</td>
                    <td>
                        <coun v-bind:obj="user" v-bind:index1="index"></coun>
                    </td>
                    <td>
                        <button @click="addFun(index)">添加到购物车</button>
                    </td>
                </tr>
                </tbody>
            </table>
    </div>
</template>

<script>
    import bus from "../bus.js";
    import coun from "./coun.vue";
   
    export default{
        components:{coun},
        data:function(){
            return{
                 users:[
                    {name:"苹果",price:5,num:0},
                    {name:"葡萄",price:3,num:0},
                    {name:"鸭梨",price:2,num:0},
                ] 
            }
           
        },
        methods:{
            clone(obj){
                var obj1={};
                for(var i in obj){
                    obj1[i]=obj[i];
                }
                return obj1;
               
            },
            addFun(dd){
                if(this.users[dd].num===0){
                   alert("数量不能为0");
                   return
                }
                var newShops=this.clone(this.users[dd]);
                bus.$emit("myeven",newShops);
            }
        },
    }
</script>

<style>
    
        .app,.foot{
            width: 50%;
            margin:0 auto;
        }
        h1,h2{
            font-family:新宋体;
        }
        div{
            margin:10px;
        }
        lable{
            font-size: 13px;
        }
        input{
            margin-left: 20px;
            width: 500px;
        }
        button{
            margin-left:10px;
            margin-right: 10px;
            background-color: rgba(19, 135, 255, 0.76);
            color: #fff;
            padding:5px 10px;
            border:1px;
        }
        table{
            width: 100%;
            border: 1px solid #b6cedb;
            border-collapse: collapse;
            margin: 0 auto;
        }
        td{
            font-size:13px;
            text-align: center;
            border: 1px solid #b6cedb;
            padding:7px 0;
        }
        tr td:nth-of-type(1){
            width:20%;
        }
        tr td:nth-of-type(2){
            width:20%;
        }
        tr td:nth-of-type(3){
            width:20%;
        }
        tr td:nth-of-type(4){
            width:40%;
        }
</style>
