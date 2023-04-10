<template>
    <div class="message">
        <p>{{ message }}</p>
    </div>
</template>

<script>
export default {
    props: {
        message: {
            type: String,
            required: true,
        }
    }
}
</script>

<style scoped>
.message p {
    color: #E86A33;
    text-align: center;
}
</style>