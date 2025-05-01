<script setup>
const props = defineProps({
    resultado: {
        type: [Number, String],
        required: true
    }
});

const alertClass = typeof props.resultado === 'number' ? 'alert-primary' : 'alert-danger';
</script>

<template>
    <div class="alert text-center fw-bold fs-4" :class="alertClass" role="alert">
        Resultado: {{ resultado }}
    </div>
</template>