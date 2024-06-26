# cc-global-components

Vue.js components for consistent navigation and branding across Creative Commons web properties

## Code of conduct

[`CODE_OF_CONDUCT.md`][org-coc]:
> The Creative Commons team is committed to fostering a welcoming community.
> This project and all other Creative Commons open source projects are governed
> by our [Code of Conduct][code_of_conduct]. Please report unacceptable
> behavior to [conduct@creativecommons.org](mailto:conduct@creativecommons.org)
> per our [reporting guidelines][reporting_guide].

[org-coc]: https://github.com/creativecommons/.github/blob/main/CODE_OF_CONDUCT.md
[code_of_conduct]: https://opensource.creativecommons.org/community/code-of-conduct/
[reporting_guide]: https://opensource.creativecommons.org/community/code-of-conduct/enforcement/


## Contributing

See [`CONTRIBUTING.md`][org-contrib].

[org-contrib]: https://github.com/creativecommons/.github/blob/main/CONTRIBUTING.md

## Status

Development: This project is currently in development.

## Overview

This project is built using [`vue-sfc-rollup`](https://www.npmjs.com/package/vue-sfc-rollup) which is is a CLI templating utility that scaffolds a minimal setup for compiling a Vue library - into a form ready to share via npm or via CDN.

The folder structure is as follows:

- `build/` : This has the rollup config for compiling files.
- `dev/`: Use for serving the components for local testing during development.
- `src`: This directory contains a sub-directory:
  - `components`: This is where our components code is found. For this project, we have three components:
    - `cc-explore.vue`: The component for the Explore CC banner.
    - `cc-global-header.vue`: The component for the Global Navigation Menus
    - `cc-global-footer.vue`: The component for the Global CC footer.
    - `index.js`: Where our components are exported. Any new component must be registered in this file.

## Components

### CC Explore

CC Explore requires a `donation-url` attribute which is the URL used for the Donation button and a `logo-url` attribute which is the location of the logo for the CC Web property this component is used on.

```html
<cc-explore
  donation-url="http://example.com"
  logo-url="/example/logo-white.png"
/>
```

### CC Global Header

The CC Global Header has three required attributes, `base-url`, `donation-url` and `logo-url`, which are the URLs used for the API call, Donation button and Logo respectively. There is one additional attribute `useMenuPlaceholders` you can set which renders placeholder Menu Items if you are in a development environment. However, if you have WordPress setup correctly and you want to test this component with real Nav Menu items, you should not pass the `useMenuPlaceholders` attribute. For a development environment, an example of a `base-url` is `http://127.0.0.1:8000`.

```html
<cc-global-header
  base-url="http://127.0.0.1:8000"
  donation-url="http:/example.com"
  use-menu-placeholders
  logo-url="/example/logo-black.png"
/>
```

### CC Global Footer

CC Global Footer requires a `donation-url` attribute which is the URL used for the Donation button and a `logo-url` attribute which is the location of the logo for the CC Web property this component is used on.

```html
<cc-global-footer
  donation-url="http://example.com"
  logo-url="/example/logo-white.png"
/>
```

#### Mixed Content Issues for the `logo-url` attribute
Mixed content occurs when initial HTML is loaded over a secure HTTPS connection, but other resources (such as images) are loaded over an insecure HTTP connection. Most modern browsers don't display pages with mixed content correctly so it is worth noting that the URL entered into the `logo-url` attribute be appropriately served over HTTPS.

## Usage

Integrate the CC Global Components into downstream projects with the following steps.

1. Add Vue JS via CDN
2. Add the stylesheets for Fonts and Vocabulary
3. Include the CC Global Components from CDN
4. Create a parent `div` element with class `container` so as to add a default left and right padding to the components. The CC-Global-Footer can be excluded from this parent element since it's required to have a full width.
5. Add the desired component(s) to your template within a container `div`
6. Render the components in the template via JavaScript

Example for the `cc-explore` component:

```html
<link
  rel="stylesheet"
  href="https://unpkg.com/@creativecommons/vocabulary-fonts@0.x.x/dist/css/fonts.css"
/>
<link
  rel="stylesheet"
  href="https://unpkg.com/@creativecommons/vocabulary-styles@0.x.x/dist/css/vocabulary-styles.css"
/>
<script src="https://unpkg.com/vue@next"></script>
<script src="https://unpkg.com/@creativecommons/cc-global-components@0.x.x/dist/cc-globals.min.js"></script>

<div class="container">
  <div id="explore-cc">
    <cc-explore
      donation-url="http://example.com"
      logo-url="/example/logo-white.png"
    />
  </div>
</div>

<script>
  const cc_explore = Vue.createApp({});
  cc_explore.use(CcGlobal);
  cc_explore.mount("#explore-cc");
</script>
```

For the `cc-global-header` component, you will need to add Axios via CDN:

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

## Development

See our [contributing guide](CONTRIBUTING.md).

## License

- [License](LICENSE)
