<template>
    <div class="display-panel">
        <v-runtime-template :template="template" />
    </div>    
</template>

<script>
import Vue from 'vue';
import { compile } from 'vue-template-compiler';
import Dropzone from '@/components/Dropzone.vue';
import VRuntimeTemplate from 'v-runtime-template';
import List from './List';
import CustomInput from './Input';
import ListItem from './ListItem';

export default {
    name: 'DisplayPanel',
    components: {
        Dropzone,
        VRuntimeTemplate,
        List,
        CustomInput,
        ListItem
    },
    computed: {
        template: {
            get() {
                return this.$store.state.template
            }
        }
    },
    mounted() {
      
    }
}
</script>

<style scoped>
.display-panel {
    overflow-y: scroll;
    height: 90vh;
}
</style>