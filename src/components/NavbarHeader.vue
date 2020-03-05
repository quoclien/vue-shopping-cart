<template>
    <div class="nav-bar">
        <h1 class="brand"> {{ Site }} </h1>
    </div>
</template>

<script>
    export default {
        name: "Sidebar",
        props: {
            Site: {
                type: String,
                required: true
            }
        }
    }
</script>

<style scoped>
    .nav-bar {
        background: linear-gradient(-90deg, #84CF6A, #16C0B0);
        height: 60px;
        margin-bottom: 15px;
    }

    .brand {
        display: inline;
        text-align: start;
    }
</style>