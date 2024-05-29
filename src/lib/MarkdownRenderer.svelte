<script lang="ts">
    import Tags from "./Tags.svelte";
    import Markdoc from "@markdoc/markdoc";
    import yaml from "js-yaml";
    import Callout from "./Callout.svelte";
    import ListView from "./ListView.svelte";


    export let doc = "";
    export let config = {};
    export let components = new Map([
        ["Callout", Callout],
        ["ListView", ListView],
    ]);


    export function add_frontmatter(ast, config) {
        const frontmatter = ast.attributes.frontmatter ? yaml.load(ast.attributes.frontmatter) : {};
        const markdoc = Object.assign(config?.variables?.markdoc || {}, { frontmatter });
        const variables = Object.assign(config?.variables || {}, { markdoc });
        return Object.assign(config, { variables });
    }

    const ast = Markdoc.parse(doc);
    const config_with_frontmatter = add_frontmatter(ast, config);
    const content: any = Markdoc.transform(ast, config_with_frontmatter);
</script>

<Tags children={content.children} {components}></Tags>
