<template>
    <drop class="dropzone" @drop="handleDrop">
    </drop>    
</template>

<script lang="ts">
import Vue,{ VNode } from 'vue';
import Component from 'vue-class-component';
import {compile} from 'vue-template-compiler';

import parser from 'snabby';
import compiler from 'snabbdom-to-html';

import { Drop } from "vue-drag-drop";
import JsBeautify from 'js-beautify';

function getRawTag(el: Vue): string {
    const tag = el.$vnode.tag;
    const parts = tag.split('-');

    // remove vue-component-number
    parts.shift();
    parts.shift();
    parts.shift();

    if (parts.length === 0) {
        parts.push(el._vnode.tag); //fixme find other way to display raw tag of vue component
    }
    return parts.join('-');
}

function getPath(el: Vue) {
  var stack = [];

  while ( el.$parent != null ) {
    var tag = getRawTag(el);
    var sibCount = 0;
    var sibIndex = 0;

    var siblings = el.$parent.$children;
    if (siblings) {
        for ( var i = 0; i < siblings.length; i++ ) {
            var sib = siblings[i];
            if ( getRawTag(sib) == tag ) {
                if ( sib === el ) {
                    sibIndex = sibCount;
                }
                sibCount++;
            }
        }
    }

    if ( sibCount > 1 ) {
      stack.unshift(tag.toLowerCase() + ':' + sibIndex);
    } else {
      stack.unshift(tag.toLowerCase());
    }
    el = el.$parent;
  }
  return stack;
}

function findNode(el: any, path: string[]): any {
    let result = el;

    while (path.length > 0) {
       
        let currentTag = path.shift();
        let sibIndex = 0;

        if (currentTag) {
            if (currentTag.indexOf(':') !== -1) {
                const parts = currentTag.split(':');
                currentTag = parts[0];
                sibIndex = Number(parts[1]);
            }
        } else {
            // idk, error?
        }


        const children = result.children;
        let foundNode = null;

        if (children) {
            let siblingsFound = 0;
            children.forEach((child: any) => {
                if (child.sel === currentTag) {
                    if (siblingsFound === sibIndex) {
                        foundNode = child;
                    }
                    siblingsFound++;
                }
            })    
        }

        result = foundNode;

    }
    return result;
}

function spawnVNode(sel: string) {
    return {
        sel,
        children: undefined,
        data: undefined,
        elm: undefined,
        key: undefined,
        text: undefined,
    }
}

@Component({
    components: {
        Drop
    }
})
export default class Dropzone extends Vue {

    public handleDrop(data: any, event: any) {
        // understand what's being dropped (which component):               check, see data.type
        // understand where is it being dropped (who is the parent):        check, kinda found by ast tree
        // write representation of what's being dropped inside the template
        // find the part in AST somehow
        // put it in

        const fullPath = getPath(this.$parent);
        const shortPath = fullPath.slice(fullPath.indexOf('v-runtime-template') + 2); // remove the root element
        //console.log(shortPath);


        const rawTemplate = this.$store.state.template;
        //console.log(rawTemplate)
        const vtree = parser(rawTemplate);  // should use native vue parser
        console.log(vtree);
        const vnode = findNode(vtree, shortPath);
        //console.log('vnode: ', vnode);

        // modify vnode (same reference)
        // vnode.add({ data.type })
        if (!vnode.children) {
            vnode.children = [];
        }
        vnode.children.push(spawnVNode(data.type));

        const template = compiler(vtree);
        //console.log(template);

        this.$store.state.template = JsBeautify.html(template);

    }
}
</script>

<style scoped>
.dropzone {
    min-height: 40px;
    border: 2px dashed green;
    margin-bottom: 0.5rem;
}
</style>