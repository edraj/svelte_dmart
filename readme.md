# DMART Frontend 

A **web-frontend** solution utilizing several technologies to deliver Content Management functionality (CMS); this allows building websites that integrate with headless CMS backend.

## Features 

- Simple file-based CMS option (compiled code) with rich and dynamic content : This is based on Svelte and Svelte Markdown with Widgets and layout control
- Multi-lingual support : Using language extension naming convention, language translations are represented in individual pages. Switching can be done by language selector or url path.
- RTL / LTR support
- I18N / L17N support
- High score page speed
- Version controlled content management flow (can be git-based)
- Integration with DMART for arbitrary content servicing (based on the customer's privileges, including world/public-access).
- DMART Entry-based rich content (markdown, media) and data content rendering

## Tech-stack 

- TypeScript / JavaScript
- Svelte 4.x
- Routify 3.x
- Bootstrap 4.x
- Vite
- DMART


## Setup

```
git clone https://github.com/edraj/svelte_dmart.git
cd svelte_dmart
yarn install
yarn build
yarn dev
```
