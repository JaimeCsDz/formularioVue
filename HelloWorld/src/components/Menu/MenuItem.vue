<template>
    <div>
        <RouterLink :to="data.path">{{ data.name }}</RouterLink>
    </div>
</template>
<script lang="ts" setup>
import type IMenuItem from '@/interface/IMenuItem';

const data = defineProps<IMenuItem>();
</script>