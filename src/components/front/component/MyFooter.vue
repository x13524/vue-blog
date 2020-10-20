<template>
    <div>
        <p>Copyright @ 2020 Powered by Vue. Designed by me | <router-link :to="{name: 'login'}" tag="span" class="login">站长登录</router-link></p>
    </div>
</template>

<script>
export default {}
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
    div {
        text-align: center;
        padding-top: 0.625rem;
        line-height: 2.5rem;
        width: 100%;
        background: rgba(55, 57, 65, 0.5);
    }
    p {
        text-align: center;
        font-size: 1rem;
    }
    span.login {
        cursor: pointer;
    }
</style>
