<template>
<header>
    <div class="wrapper">
        <h1>Employee Management System</h1>
        <nav>
            <RouterLink to="/">Home</RouterLink>
            <RouterLink to="/about">About</RouterLink>
        </nav>
    </div>
</header>
<RouterView />
</template>




<script lang="ts">
import {
    RouterLink,
    RouterView
} from 'vue-router'

export default{

}

</script>








<style>
header {
    background-color: #333;
    color: #fff;
    padding: 10px;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 100;
}

.wrapper {
    max-width: 960px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

nav a {
    color: #fff;
    text-decoration: none;
    margin-right: 50px;
}

nav a {
    color: white;
    text-decoration: none;
    transition: all 0.2s ease-in-out;
}

nav a:hover {
    color: aqua;
    box-shadow: 0 2px 4px rgb(92, 225, 248);
}
</style>
