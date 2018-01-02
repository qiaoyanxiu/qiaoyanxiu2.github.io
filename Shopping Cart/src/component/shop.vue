<template>
   <div class="foot">
        <h2>购物车</h2>
        <table>
            <thead>
                <tr>
                    <td>商品信息</td>
                    <td>单价</td>
                    <td>数量</td>
                    <td>操作</td>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(shop,index) in shops">
                    <td>{{shop.name}}</td>
                    <td>{{shop.price}}</td>
                    <td>
                        <coun v-bind:obj="shop" v-bind:index1="index"></coun>
                    </td>
                    <td>
                        <button @click="fun2(index)">删除</button>
                    </td>
                </tr>
                <tr>
                    <td colspan="4">
                        <button @click="sum1()">总价</button>
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
                shops:[]
            }
        },
        methods:{
            fun2(cc){
                this.shops.splice(cc,1);
            },
            sum1(){
                var sum=0;
                for(var g=0;g<this.shops.length;g++){
                    sum=sum+this.shops[g].price*this.shops[g].num;
                }
                alert(sum)
            }
        },
        mounted:function(){
            var self=this;
            bus.$on("myeven",function(data){
               for(var j=0;j<self.shops.length;j++){
                   if(data.name===self.shops[j].name){
                       self.shops[j].num=self.shops[j].num+data.num;
                       return;
                   }
               }
               self.shops.push(data);
            }) 
        }
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