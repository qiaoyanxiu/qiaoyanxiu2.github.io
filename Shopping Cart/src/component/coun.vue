<template>
    <div>
        <button @click="obj.num?obj.num--:0">-</button>
            {{obj.num}}
        <button @click="obj.num++">+</button>
    </div>
</template>
 <script>
     export default{
         props:["obj","index1"],
     }
</script>       