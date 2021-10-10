<template>
    <footer id="footer">
        <p>Make Your burger &copy; 2021</p>
    </footer>
</template>


<script>
export default {
    name: "Footer"
}
</script>



<style scoped>
    #footer {
        height: 200px;
        background-color: var(--primary-color);
        border-top: 4px var(--border-color);
        color: var(--secundary-color);;
        display: flex;
        justify-content: center;
        align-items: center;
       /*  position: absolute;
        bottom: 0; */
        width: 100%;
    }
</style>