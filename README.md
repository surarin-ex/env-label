# Env Label

During development, have you operated on your production page that was open at the same time by mistake?

*Env Label* will save you from such a mistake.

![image](https://user-images.githubusercontent.com/1811616/37532798-6507d982-2983-11e8-99a5-7099165ae66d.png)

## Usage

Just install and call `init` method to set up in your code.

### Step1. Installation

```shell
$ npm install --save env-label
or
$ yarn add env-label
```

### Step2. Initialize

#### Use as ES module

```javascript
import EnvLabel from 'env-label';

EnvLabel.init({
  conditions: [
    {regex: /localhost/,    labelText: 'development', labelColor: '#00aaaa'},
    {regex: /example\.com/, labelText: 'edge', labelColor: '#aaaa00'},
  ]
});
```

#### Load through `<script>` tag

```html
<script type="text/javascript" src="path/to/dist/js/env-label.js"></script>
<script type="text/javascript">
    // initialize with conditions
    window.EnvLabel.init({
      conditions: [
        {regex: /localhost/,    labelText: 'development', labelColor: '#00aaaa'},
        {regex: /example\.com/, labelText: 'edge', labelColor: '#aaaa00'},
      ]
    });
</script>
```

That's all!

### (Optional) Skip set up in some environment

If you don't want to run `env-label` on production, just skip the initialization on build or runtime.

```javascript
if (!process.env.DISABLE_ENV_LABEL) {
  EnvLabel.init({ ... });
}

// or

if (anyCondition) {
  EnvLabel.init({ ... });
}
```

## Configuration Options

#### `EnvLabel.init({ conditions: Array<Condition> }): void`

It initializes `EnvLabel` based on `conditions` parameter. The `conditions` should be like below.

#### `Condition`

Parameter | Required | Type | Description
--- | --- | --- | ---
regex | true | `RegExp` | A regex to test against `window.location.hostname`. If it matches, a label appears.
labelText | false | `string` | Text that you want to show on a label.
labelColor | false | `string` | Color of label.