<script setup>

</script>

<template>
    <ul>
        <li>Пациент 1</li>
        <li>Пациент 2</li>
        <li>Пациент 3</li>
    </ul>
    <form action="">
        <input type="text" placeholder="Имя">
        <input type="text" placeholder="Фамилия">
        <input type="text" placeholder="Отчество">
        <input type="date" placeholder="Дата рождения">
        <input type="tel" placeholder="Телефон">
        <input type="email" placeholder="Email">
    </form>
</template>

<style>
html {
    margin: 0;
    padding: 0;
    overflow: hidden;
}
body {
    background: #3f3f3f;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100vh;
}
ul {
    list-style: none;
    padding: 0;
    display: flex;
    gap: 15px;
    margin: 0 0 30px;
}
li {
    background: #220036;
    padding: 5px 10px;
    border-radius: 15px;
    color: #fff;
    cursor: pointer;
    font-size: 18px;
}
li.active,
li:hover {
    background: #540085;
}
form {
    width: 500px;
    display: flex;
    flex-direction: column;
    gap: 15px;
    color: black;
}
input {
    padding: 10px;
    border-radius: 5px;
    font-size: 16px;
    border: none;
    outline: aqua;
    font-family: 'Helvetica', 'Arial', sans-serif;
}
</style>
