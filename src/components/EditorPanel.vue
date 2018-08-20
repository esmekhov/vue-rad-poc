<template>
    <div class="editor-panel">
        <codemirror v-model="content" :options="options"></codemirror>
    </div>    
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
import { codemirror } from 'vue-codemirror';
import 'codemirror/lib/codemirror.css';

@Component({
    components: {
        codemirror
    }
})
export default class EditorPanel extends Vue {

    private get content() {
        return this.$store.state.template;
    }

    private set content(value) {
        this.$store.state.template = value;
    }

    private options = {
        // codemirror options
        tabSize: 4,
        mode: 'text/x-vue',
        lineNumbers: true,
        line: true,
    }


    // the goal here is to work with the storage to receive new elements and display them
    // stuff that is typed here goes to the storage, from where it goes to the display zone

}
</script>

<style scoped>
</style>