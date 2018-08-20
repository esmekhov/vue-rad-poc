<template>
    <input class="input" />
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';

import { Prop } from 'vue-property-decorator';

@Component({
    components: {
    }
})
export default class CustomInput extends Vue {

    @Prop({ default: true }) private editMode!: boolean;
}
</script>

<style scoped>
</style>