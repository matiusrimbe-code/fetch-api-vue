<template>
    <nav>
        <RouterLink class="btn-link" to="/">Home</RouterLink>
        <RouterLink class="btn-link" to="/about">About</RouterLink>
    </nav>
</template>

<style scoped>
nav {
    display: flex;
    align-items: center;
    justify-content: start;
    gap: 10px;
    margin-bottom: 30px;
}

.btn-link {
    padding: 10px 20px;
    text-decoration: none;
    background-color: gray;
    color: #fff;
    border-radius: 10px;
}
</style>