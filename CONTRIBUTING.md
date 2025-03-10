# Contributing

There are many ways to contribute to this project such as testing, design, and development.

## Code of Conduct

By participating in this project, you are expected to uphold our [Code of
Conduct][code_of_conduct].

## Development

This section provides information for people who are interested in contributing code.

### Setup

Fork this repository and clone it to your local development environment.
In the root folder (`cc-global-components`), run the following commands:

```npm
npm install
```

To preview the project ([localhost:8080/](http://localhost:8080/)), run

```npm
npm run serve
```

To build the project, run

```npm
npm run build
```

To build the project just for CDN use, run

```npm
npm run build:unpkg
```

### Testing Locally

To test locally how it will behave when hosted on a CDN, serve the file `example.html` found in the root directory.
To include the components in an HTML template:

- Add Vue JS via CDN
- Add the stylesheets for Fonts and Vocabulary
- Add the build version of the components via a script tag (the output of `npm run build:unpkg`)
- Import each component, passing it's respective attribute as such and mount it on a corresponding `div` element.
  - CC Global Header has two required attributes, `base-url` and `donation-url` , which are the URLs used for the API call and the Donation button respectively. For a development environment, the `base-url` could be `http://127.0.0.1:8000`.
    - `<cc-global-header base-url="http://127.0.0.1:8000" donation-url="http:/example.com" />`
  - CC Global Footer and CC Explore have just one required attribute each, a `donation-url` attribute which is the URL used for the Donation buttons.
    - `<cc-global-footer donation-url="http://example.com" />`
    - `cc-explore donation-url="http://example.com" />`

**Note:** Wrap the components in a parent `div` element with class `container` so as to add a default left and right padding to the components. The CC-Global-Footer can be excluded from this parent element since it's required to have a full width.

Example for the `cc-explore` component:

```html
<link
  rel="stylesheet"
  href="https://unpkg.com/@creativecommons/fonts@2020.9.3/css/fonts.css"
/>
<link
  rel="stylesheet"
  href="https://unpkg.com/@creativecommons/vocabulary@2020.11.3/css/vocabulary.css"
/>
<script src="https://unpkg.com/vue@next"></script>
<script src="./dist/cc-global.min.js"></script>

<div class="container">
  <div id="explore-cc">
    <cc-explore donation-url="http://example.com" />
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

In your development setup, we have a `useMenuPlaceholders` attribute you can pass to the CC Global Header element to render placeholder Menu items.

```html
<cc-global-header donation-url="http://example.com" use-menu-placeholders />
```

## Publishing a release

Use the following steps when publishing a new CC Global Components release.

1. Choose a release number using [semantic versioning](https://semver.org/)
2. [Update the project version](https://docs.npmjs.com/updating-your-published-package-version-number) with `npm version <update_type>`
3. Run `npm install` to automatically update project metadata in `package-lock.json`
4. Merge the project metadata changes into the `main` branch
5. Create a new release/tag on GitHub from the latest commit in `main`
   - use only the version number as the tag (without any prefix or suffix)
6. Build the project for NPM/unpkg with `npm run build:unpkg`
7. Run `npm publish` to publish latest version on NPM
