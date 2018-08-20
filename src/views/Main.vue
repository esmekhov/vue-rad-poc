<template>
  <div class="main">
    <div class="left">
        <toolbar />
        <display-panel />
    </div>
    <div class="right">
        <editor-panel />
        <model-panel />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import EditorPanel from '@/components/EditorPanel.vue';
import ModelPanel from '@/components/ModelPanel.vue';
import Toolbar from '@/components/Toolbar.vue';
import DisplayPanel from '@/components/DisplayPanel.vue';

@Component({
  components: {
    ModelPanel,
    EditorPanel,
    DisplayPanel,
    Toolbar
  },
})
export default class Main extends Vue {}
</script>

<style scoped>
.main {
    display: flex;
    flex-direction: row;
}

/* don't use flex, you're just setting yourself up. use grid */

.left {
    flex: 0 0 50%;
}

.right {
    flex: 0 0 50%;
}
</style>