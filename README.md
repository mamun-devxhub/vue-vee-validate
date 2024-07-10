# @mdxh/vee-validate

Install VeeValidate to vue3 using dxh wrapper

## Usage

### Installation

Just use the below command to install VeeValidate.

```sh
npm i @mdxh/vee-validate@latest
```

This command will install `vee-validate` and `@vee-validate/rules` automatically.

### Plugin Configaration with validation rules

You can add below code to main.ts:

```sh
import { defineRule, configure } from 'vee-validate'
import { all } from '@vee-validate/rules'

type ValidationMessages = {
  [key: string]: string;
};

Object.entries(all).forEach(([name, rule]) => {
  defineRule(name, rule)
})

defineRule("phone", (value: any) => {
  const regex = /^\+?[0-9](?:[0-9 ]{5,}[0-9])$/;
  if (regex.test(value)) {
    return true;
  }
  return "The field must be a valid phone number.";
});

configure({
  bails: false,
  validateOnInput: true,
  validateOnBlur: true,
  validateOnChange: true,
  generateMessage: (context) => {
    const field = context.label || context.field;
    const ruleName = context.rule?.name;
    const params = (context.rule?.params as unknown[]) || [];

    const messages: ValidationMessages = {
      required: `The field ${field} is required.`,
      email: `The field ${field} must be a valid email.`,
      alpha: `The field ${field} may only contain alphabetic characters`,
      alpha_dash: `The field ${field} may contain alpha-numeric characters as well as dashes and underscores`,
      alpha_num: `The field ${field} may only contain alpha-numeric characters`,
      alpha_spaces: `The field ${field} may only contain alphabetic characters and spaces`,
      between: `The field ${field} must be between ${params[0]} and ${params[1]}`,
      confirmed: `The field ${field} does not match`,
      digits: `The field ${field} must be numeric and exactly contain ${params[0]} digits`,
      dimensions: `The field ${field} must be between ${params[0]} and ${params[1]} pixels`,
      not_one_of: `The field ${field} contains an invalid value`,
      ext: `The field ${field} must have a valid file extension`,
      image: `The field ${field} must be an image`,
      one_of: `The field ${field} must be one of the allowed values`,
      integer: `The field ${field} must be an integer`,
      is: `The field ${field} must be ${params[0]}`,
      is_not: `The field ${field} must not be ${params[0]}`,
      length: `The field ${field} must be exactly ${params[0]} characters long`,
      max: `The field ${field} may not be greater than ${params[0]} characters`,
      max_value: `The field ${field} must be ${params[0]} or less`,
      mimes: `The field ${field} must have a valid MIME type`,
      min: `The field ${field} must be at least ${params[0]} characters`,
      min_value: `The field ${field} must be ${params[0]} or more`,
      numeric: `The field ${field} may only contain numeric characters`,
      regex: `The field ${field} format is invalid`,
      size: `The field ${field} size must be less than ${params[0]}KB`,
      url: `The field ${field} must be a valid URL`,
    };

    if (ruleName && messages[ruleName]) {
      return messages[ruleName];
    }

    return `The field ${field} is invalid.`;
  },
});
```

Now you can use VeeValidate in your components

### Start your project

```sh
npm run dev
```

## VeeValidate Documentation

See [VeeValidate Documentation](https://vee-validate.logaretm.com/v4/tutorials/basics/).

See [VeeValidate Global Rules](https://vee-validate.logaretm.com/v4/guide/global-validators/).
