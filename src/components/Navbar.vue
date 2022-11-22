<template>
    <div class="navbar">
        <div @click="$router.push('/')" class="navbar__logo">VUE 3</div>
        <div class="navbar__btns">
            <my-button @click="$router.push('/posts')">Список постов</my-button>
            <my-button @click="$router.push('/store')" class="navbar__btns-r">Store</my-button>
            <my-button @click="$router.push('/about')"  class="navbar__btns-r">О приложении</my-button>
        </div>
    </div>
</template>

<script>

</script>


<style scoped>
.navbar {
    background: rgb(246, 222, 246);
    box-shadow: 2px 2px 4px rgb(198, 190, 198);
    display: flex;
    align-items: center;
    padding: 15px;
}
.navbar__logo {
    font-weight: bold;
}
.navbar__btns {
    margin-left: auto;
}
.navbar__btns-r {
    margin-left: 15px
}
</style>
