<template>
    <header class="header">
        <h1 class="logo">My Todo</h1>
        <p class="date">{{timestamp}}</p>
    </header>
</template>
<script>
export default {
    name: 'TodoHeader',
    data(){
        return{
            timestamp: ""
        }
    }
}
</script>