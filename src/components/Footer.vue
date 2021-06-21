<template>
    <footer>
        <p>Copyright</p>
        <router-link to="/about">About</router-link>
    </footer>

</template>

<script>
export default {
    name:'Footer'
}
</script>

<style scoped>
    a, p{
        color: white;
    }    

    footer{
        margin-top: 30px;
        text-align: center;
        background-color: #484848;
    }
</style>