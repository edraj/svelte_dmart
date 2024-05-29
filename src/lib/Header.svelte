<script lang="ts">
  import {Navbar, NavbarBrand, Nav, NavLink, NavItem} from "sveltestrap";
  import { _ } from "@/i18n";
  import { user, signout } from "@/stores/user";
  import markdownFiles from "@/md_indexer.json";
  import {goto} from "@roxi/routify";


  let term = '';
  let suggestions = [];
  let delayTimer;
  async function handleInputChange(event: any) {
      console.log('handleInputChange', event.target.value);
      clearTimeout(delayTimer);
      delayTimer = setTimeout(async function() {
          console.log('searching for', event.target.value);
          suggestions = [];
          term = event.target.value;
          if (term===""){
              return;
          }
          const _term = term.toLowerCase();
          for (const file of markdownFiles) {
              try {
                  const _result = file.content.toLowerCase();
                  if (_result.includes(_term)) {
                      suggestions = [
                          ...suggestions,
                          {
                              path: file.path,
                              title: file.filename.replace('.md', '').replace(/-/g, ' ').replace("index", "Home"),
                              description: "..."+_result.substring(
                                  _result.indexOf(_term)-50, _result.indexOf(_term)+50
                              ).replace(_term.toLowerCase(), "<b>"+_term+"</b>")+"..."
                          }
                      ];
                  }
              } catch (e) {
              }
          }
      }, 1000);
  }

  function handleSuggestionClick(suggestion: any) {
      $goto(`${suggestion.path.replace('.md', '')}`);
      suggestions = [];
  }

</script>

<Navbar color="light" light expand="md" class="px-2 py-0"
        style="border-bottom: solid #cecece">
  <NavbarBrand href="/" title="{$_('home')}">{$_('home')}</NavbarBrand>
  <Nav navbar class="d-flex justify-content-between" style="width: 100%">
    {#if $user && $user.signedin}
      <NavItem class="d-flex align-items-center">{$user.localized_displayname}</NavItem>
    {/if}
    <NavItem class="w-75 align-content-center">
    <div class="container">
      <div class="position-relative">
        <input type="text" class="form-control" placeholder="Search..."
         bind:value={term}
         on:input={handleInputChange}
         on:focusout={()=>{
            setTimeout(()=>{suggestions = [];}, 200);
         }}
         on:focusin={handleInputChange}>
        {#if suggestions.length > 0}
          <ul class="list-group suggestion-list">
            {#each suggestions as suggestion}
              <!-- svelte-ignore a11y-no-noninteractive-element-interactions a11y-click-events-have-key-events -->
              <li class="search-item list-group-item" on:click={() => handleSuggestionClick(suggestion)}>
                <h5>{suggestion.title}</h5>
                {@html suggestion.description}
              </li>
            {/each}
          </ul>
        {/if}
      </div>
    </div>
    </NavItem>
    {#if !$user || !$user.signedin}
      <NavLink href="/login" title="{$_('login')}">{$_('login')}</NavLink>
    {:else}
      <NavLink href="#" title="{$_('logout')}" on:click="{signout}"> {$_('logout')} </NavLink>
    {/if}
  </Nav>
</Navbar>
<style>
    .search-item:hover {
        background-color: #ccc;
    }
    .search-item {
        cursor: pointer;
    }
    .suggestion-list {
        position: absolute;
        z-index: 2;
        width: 100%;
        background-color: white;
        border: 1px solid #ccc;
    }
</style>