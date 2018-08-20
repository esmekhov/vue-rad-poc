<template>
    <div class="list-item">
        List item text!
    </div>    
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';

import { Prop } from 'vue-property-decorator';
@Component({
    components: {
    }
})
export default class ListItem extends Vue {

}
</script>

<style scoped>
</style>