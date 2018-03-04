---
layout: page
title: Alias
---

{% raw %}
### Methods


<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

-   [alias](#alias)

### alias

Returns the value of some other property on the PageObject.

**Parameters**

-   `pathToProp` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** dot-separated path to a property specified on the PageObject
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)**  (optional, default `{}`)
    -   `options.chainable` **[Boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** when this is true, an aliased
        method returns the PageObject node on which the alias is defined, rather
        than the PageObject node on which the aliased property is defined.

**Examples**

```javascript
import { create } from 'ember-cli-page-object';
import { alias } from 'ember-cli-page-object/macros';

const page = create({
  submitButton: {
    scope: '.submit-button'
  },
  submit: alias('submitButton.click')
});

// calls `page.submitButton.click`
page.submit();
```

```javascript
import { create } from 'ember-cli-page-object';
import { alias } from 'ember-cli-page-object/macros';

const page = create({
  submitButton: {
    scope: '.submit-button'
  },
  isSubmitButtonVisible: alias('submitButton.isVisible')
});

// checks value of `page.submitButton.isVisible`
assert.ok(page.isSubmitButtonVisible);
```

```javascript
import { create } from 'ember-cli-page-object';
import { alias } from 'ember-cli-page-object/macros';

const page = create({
  form: {
    input: {
      scope: 'input'
    },
    submitButton: {
      scope: '.submit-button'
    }
  },
  fillFormInput: alias('form.input.fillIn', { chainable: true }),
  submitForm: alias('form.submitButton.click', { chainable: true })
});

// executes `page.form.input.fillIn` then `page.form.submitButton.click`
// and causes both methods to return `page` (instead of `page.form.input`
// and `page.form.submitButton` respectively) so that the aliased methods
// can be chained off `page`.
page
  .fillFormInput('foo')
  .submitForm();
```

-   Throws **any** Will throw an error if the PageObject does not have the specified property.

Returns **Descriptor** 
{% endraw %}