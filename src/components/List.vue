<template>
    <div class="list">
        <slot />
        <template v-if="editMode">
            <dropzone />
        </template>
    </div>    
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';

import { Prop } from 'vue-property-decorator';
import Dropzone from './Dropzone.vue';

@Component({
    components: {
        Dropzone
    }
})
export default class List extends Vue {

    @Prop({ default: true }) private editMode!: boolean;
}
</script>

<style scoped>
.list {
    padding-left: 0.5rem;
}
</style>