<script lang="ts">
    import {
        Row,
        Col,
        Card,
        CardBody
    } from 'sveltestrap';
    import {url} from "@roxi/routify";
    import Footer from "@/lib/Footer.svelte";
    import Header from "@/lib/Header.svelte";

    const docFiles = [
        'index.md',
        'Charts.md',
        'Widgets.md',
    ];

    let selectedIndex = docFiles.findIndex(file => `/docs/${file.replace('.md', '').replace('index','')}`===window.location.pathname );
</script>

<style>
    @import "prismjs/themes/prism.css";
    @import "prismjs/themes/prism-coy.css";
</style>

<Header />
<Row class="mx-auto">
  <Col sm="2" class="d-flex bg-light" style="overflow-y: auto; padding: 0px!important;border-right: solid #cecece;">
      <ul class="nav nav-pills flex-column" style="height:95vh;width: 100%;padding-top: 16px;">
        {#key $url}
          {#each docFiles as file, index}
            <!-- svelte-ignore a11y-no-noninteractive-element-interactions a11y-click-events-have-key-events -->
            <li
              on:click={()=> selectedIndex = index}
              class={
                file===docFiles[selectedIndex]
                ? "nav-item selected px-2" : "nav-item px-2"
              }>
              <a href="{file.replace('.md', '').replace('index','/')}" class="nav-link link-dark">
                {file.replaceAll('-', ' ').replace('.md', '').replace('index','Why Dmart ?')}
              </a>
            </li>
            <hr class="p-0 m-0">
          {/each}
        {/key}
      </ul>
      <style>
        .selected {
            background-color: #e5e5e5;
        }
      </style>
  </Col>
  <Col sm="10" style="padding: 0.5rem;">
    <Card class="px-4" style="overflow-y: auto; height:89vh">
      <CardBody>
        <slot/>
      </CardBody>
    </Card>
  </Col>
</Row>
<div class="fixed-bottom">
  <Footer />
</div>
