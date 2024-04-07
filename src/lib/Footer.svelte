<script lang="ts">
  import { Navbar, NavbarBrand } from "sveltestrap";
  import SelectLanguage from "./SelectLanguage.svelte";
  import Icon from "./Icon.svelte";
</script>

<Navbar class="px-3" color="light" light style="border-top: solid #cecece">
  <SelectLanguage />
</Navbar>
