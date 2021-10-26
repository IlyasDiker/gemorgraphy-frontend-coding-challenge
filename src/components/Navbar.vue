<template>
    <nav class="navbar">
        <span class="navbar-logo">Gemophraphy-frontend-challenge</span>
    </nav>
</template>

<script>
export default {
    name: "Navbar",
    
}
</script>

<style lang="less">
    .navbar{
        position: fixed;
        top: 0;
        right: 0;
        left: 0;
        padding: 20px;
        color: white;
        background: rgba(0, 0, 0, 0.445);
        backdrop-filter: blur(20px);
        -webkit-backdrop-filter: blur(20px);
        border-bottom: 1px solid rgba(245, 245, 245, 0.247);

        .navbar-logo{
            font-size: 1rem;
        }
    }
</style>