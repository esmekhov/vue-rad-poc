<template>
    <nav class="toolbar">
        <draggable :transferData="{ type: 'custom-input'}">
            <div>Input</div>
        </draggable>
        <draggable :transferData="{ type: 'list' }">
            <div>List</div>
        </draggable>
        <draggable :transferData="{ type: 'list-item' }">
            <div>List Item</div>
        </draggable>
    </nav>    
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';

import Draggable from '@/components/Draggable.vue';

@Component({
    components: {
        Draggable
    }
})
export default class Toolbar extends Vue {

}
</script>

<style scoped>
.toolbar {
    display: flex;
    flex-direction: row;
    height: 5vh;
}

.toolbar > * {
    flex: 1 1 auto;
}
</style>
