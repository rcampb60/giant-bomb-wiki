# Contributing to The Giant Bomb Wiki

Thanks for your interest in contributing! This project uses MediaWiki with custom skins and Vue components. Below are guidelines to help you get started.

## Development

To get started fork the repo and make your changes then compare to the main branches for PRs.

## Code Formatting

We use [Prettier](https://prettier.io/docs/install) and `.editorconfig` to enforce formatting rules.

Make sure your code editor is configured to use Prettier as the default formatter.

## Working with Skins

### Enabling the Giant Bomb Skin

In your `LocalSettings.php`, add:

```php
wfLoadSkin( 'GiantBomb' );
$wgDefaultSkin = "giantbomb";
```

You can manage available skins via `LocalSettings.php`. See the [MediaWiki manual](https://www.mediawiki.org/wiki/Manual:LocalSettings.php) for more details.

## Building Vue Components

Vue components can be created either as `.js` (using SFC syntax) or `.vue` files.

### JavaScript Resource Module (`.js`)

- Add `.js` files to:  
  `/skins/GiantBomb/resources/components/`

- Example:  
  `VueExampleComponent.js`

- Register the component in `skin.json` under a new Resource Module:
  ```json
  "skin.giantbomb.vueexamplecomponent": {
    "scripts": [ "resources/components/VueExampleComponent.js" ]
  }
  ```

### Vue Single File Component (`.vue`)

- Add `.vue` files to:  
  `/skins/GiantBomb/resources/components/`

- Example:  
  `VueSingleFileComponentExample.vue`

- Register it in `skin.json` under `skins.giantbomb` as a `packageFile`.

## Binding Vue Components

To bind components to HTML within PHP templates:

1. Ensure the component is loaded via `index.js`:

   ```js
   import VueExampleComponent from "./VueExampleComponent.js";
   export default {
     "vue-example-component": VueExampleComponent,
   };
   ```

2. In your `.php` templates (e.g. `GiantBombTemplate.php`), use:

   ```html
   <div
     data-vue-component="vue-example-component"
     data-title="Game Title"
   ></div>
   ```

3. Props are passed using `data-` attributes in kebab-case:
   ```html
   data-game-id="123" data-my-prop="value"
   ```

### Using Vue Components Within Other Components

You can import and nest components like so:

```js
const SubComponent = require("./SubComponent.vue");
export default {
  components: { SubComponent },
};
```

## Project TODOs

Here are some open contributor tasks:

- ~~Remove files that can be regenerated via the MediaWiki CLI~~
- Start on proof-of-concept approaches for wiki theming
- Start on building out complex relationships between categories
