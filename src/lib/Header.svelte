<script lang="ts">
  import {Navbar, NavbarBrand, Nav, NavLink, NavItem} from "sveltestrap";
  import { _ } from "@/i18n";
  import { user, signout } from "@/stores/user";
</script>

<Navbar color="light" light expand="md" class="px-2 py-0"
        style="border-bottom: solid #cecece">
  <NavbarBrand href="/" title="{$_('home')}">{$_('home')}</NavbarBrand>
  <Nav navbar class="d-flex justify-content-between" style="width: 100%">
    {#if $user && $user.signedin}
      <NavItem>{$user.localized_displayname}</NavItem>
    {/if}
    {#if !$user || !$user.signedin}
      <NavLink href="/login" title="{$_('login')}">{$_('login')}</NavLink>
    {:else}
      <NavLink href="#" title="{$_('logout')}" on:click="{signout}"> {$_('logout')} </NavLink>
    {/if}
  </Nav>
</Navbar>
