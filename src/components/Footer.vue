<template>
    <footer id="footer">
        <p>Make Your Burger &copy; 2023</p>
    </footer>
</template>
<script>
import { defineComponent } from "vue"


export default defineComponent({
    name: 'Footer'
})
</script>

<style scoped>
    #footer{
        grid-area: footer;

        height: 200px;
        background-color: #222;
        border-top: 4px solid #111;
        color: #fcba03;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;

    }
</style>
