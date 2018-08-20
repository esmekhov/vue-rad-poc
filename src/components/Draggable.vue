<template>
    <drag :transfer-data="transferData">
        <slot />
    </drag>
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
import { Prop } from 'vue-property-decorator';

import { Drag } from "vue-drag-drop";

@Component({
    components: {
        Drag
    }
})
export default class Draggable extends Vue {

    @Prop() private transferData: any;
}
</script>

<style scoped>

</style>