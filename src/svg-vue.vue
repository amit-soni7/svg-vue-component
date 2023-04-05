Skip to content
Search or jump to…
Pull requests
Issues
Codespaces
Marketplace
Explore
 
@amit-soni7 
danielstgt
/
svg-vue3
Public
Fork your own copy of danielstgt/svg-vue3
Code
Issues
1
Pull requests
Actions
Projects
Security
Insights
svg-vue3/src/svg-vue.vue
@danielstgt
danielstgt use all attributes from svgo string
Latest commit dc8414f on Aug 15, 2021
 History
 1 contributor
40 lines (31 sloc)  1.1 KB
 

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
        const svgString = computed(() => require(`./resources/svg/${iconPath.value}`).default);
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