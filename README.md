# 💄 glamorous  → 👩‍🎤 emotion
This codemod was created to help migrate an existing React or Preact codebase from [glamorous](https://github.com/paypal/glamorous) to [emotion](https://github.com/emotion-js/emotion) in light of [this issue](https://github.com/paypal/glamorous/issues/419) on glamorous.

## Features
This codemod follows the [glamorous to emotion migration guide](https://github.com/paypal/glamorous/blob/master/other/EMOTION_MIGRATION.md) on the glamorous repo. Particularly, it rewrites the following:

- ✅ All import statements, including ThemeProvider inclusion.
- ✅ All glamorous function calls to emotion function calls.
- ✅ The content property to be emotion friendly.

## Usage
You'll need to use [`babel-codemod`](https://github.com/square/babel-codemod) to apply this codemod to your existing codebase. It should be pretty straightforward:

- First, install this plugin: `yarn add babel-plugin-glamorous-to-emotion -D`

- Then run it: `npx babel-codemod --plugin babel-plugin-glamorous-to-emotion "src/**/*.js"` or a similar variation depending on your directory structure.

This will put you fully in emotion-land.

### Options

You may also pass `--plugin-options` to the `babel-codemod` command. Here's a sample call:

```
npx babel-codemod --plugin babel-plugin-glamorous-to-emotion --plugin-options glamorousToEmotion='{"mode": "withBabelPlugin"}' src/**/*.js
```

- #### `mode`

  This plugin offers three modes to convert your glamorous code.

  Let's compare them based on this glamorous snippet

  ```jsx
  <glamorous.Div marginTop={5} />
  ```

  ##### `{"mode": "withJsxPragma"}` (default)

  If you can't or don't want to add emotion's [@emotion/babel-preset-css-prop](https://emotion.sh/docs/@emotion/babel-preset-css-prop), you can use emotion via setting the jsx pragma. This will create code like this:

  ```jsx
  /** @jsx jsx */
  import { jsx } from "@emotion/core";

  <div css={{marginTop: 5}} />
  ```

  ##### `{"mode": "withBabelPlugin"}`

  Use this option if you are able to use the babel plugin. The resulting code will look like this:

  ```jsx
  <div css={{marginTop: 5}} />
  ```

  ##### `{"mode": "className"}`

  If neither is an option for you, this codemod allows you to directly set the `className` instead:

  ```jsx
  import { css } from "@emotion/core";

  <div className={css({marginTop: 5})} />
  ```


- #### `{"preact": true}`

  Uses `import styled from "@emotion/preact-styled"` instead of `import styled from "@emotion/styled"`


## Contributing
### ALL CONTRIBUTIONS WELCOME!
I sincerely hope it helps you migrate your codebase! Please open issues for areas where it doesn't quite help and we'll sort it out.

## Acknowledgements
The following people are awesome for their open source work and should be acknowledged as such.

- [@tkh44](https://github.com/tkh44) for writing emotion.
- [@kentcdodds](https://github.com/kentcdodds) for writing glamorous.
- [@cbhoweth](https://github.com/cbhoweth), [@coldpour](https://github.com/coldpour), [@mitchellhamilton](https://github.com/mitchellhamilton), [@roystons](https://github.com/roystons) for writing the migration guide.
- [@jamiebuilds](https://github.com/jamiebuilds) for an incredible [Babel handbook](https://github.com/jamiebuilds/babel-handbook/blob/master/README.md).
