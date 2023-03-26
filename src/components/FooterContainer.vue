<template>
    <footer>
        <h4>Łukasz Oleś</h4>
        <div class="links">
        <a href="https://github.com/lukor5?tab=repositories"><i class="fab fa-github" /></a>
        <a href="https://www.linkedin.com/in/lukor5/"><i class="fab fa-linkedin"/></a>
        </div>
    </footer>
</template>

<script>
export default {
    name: 'SearchContainer'
}
</script>

<style lang="scss" scoped>
footer {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding-inline: 20px;
    align-items: center;
    background-color: black;
}

.links i {
    padding: 10px;
}

.links a {
    color: white;
}
</style>