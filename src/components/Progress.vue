<script lang="js" setup>

    defineProps({
        value: Number,
        max: Number
    });
</script>

<template>
    <div class="progress">
        Etape {{ value + 1 }} sur {{ max + 1 }}
        <progress :max="max" :value="value">
        </progress>
    </div>
</template>