<template>
    <svg
        v-bind="svgAttributes"
        v-html="svgContent"
    >
    </svg>
</template>

<script>
import { computed } from 'vue';

export default {
    name: 'SvgVue',
    props: {
        icon: String
    },
   setup(props) {
        const iconPath = computed(() => props.icon.replace(new RegExp('.'.replace(/([.*+?^=!:${}()|\[\]\/\\])/g, '\\$1'), 'g'), '/') + '.svg');
        const svgString =  computed(() => importString());
        async function importString() {
           return await import(`'svg-files-path'/${iconPath.value}`).default
        }
        const svgAttributes = computed(() => {
            if (! svgString) return {};
            let wrapper = document.createElement('div');
            wrapper.innerHTML = svgString.value;
            let attributesList = wrapper.firstElementChild.attributes;
            let attributes = {};
            Object.keys(attributesList).map(i => attributes[attributesList[i].name] = attributesList[i].value);
            return attributes;
        });
        const svgContent = computed(() => svgString ? svgString.value.replace(/^<svg[^>]*>|<\/svg>$/g, '') : null);
        return { svgAttributes, svgContent };
    }
}
</script>
Footer
© 2023 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
svg-vue3/svg-vue.vue at master · danielstgt/svg-vue3