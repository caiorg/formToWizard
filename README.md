# formToWizard

Turn any webform into multi-step wizard with jQuery.


### Features

Every form fieldset becomes a separate "step" with forward and back buttons, gracefuly degrading if no script available.


### History

First, there was an amazing [tutorial from Janko][1]. Unfortunately there isn't a code repository and example comes without field validation.

Second, it was inherited by [tutorial from iFadey][2]. As for now, breadcrumbs is optional and plugin uses [Validation Engine][3] for step validation. There's no public repo too.

User [artoodetoo][5] made it neat, replaced hardcoded things with callbacks and options and published a [repository at GitHub][6] with couple of examples, from which this repo is forked.  


### Sample code

To use [jQuery Validation][4] plugin and see progress as growing color bar, do something like that:

```js
var $signupForm = $( '#SignupForm' );

$signupForm.validate(); 

$signupForm.formToWizard({
    submitButton: '#SaveAccount',
    nextBtnName: 'Forward >>',
    prevBtnName: '<< Previous',

    validateBeforeNext: function(form, step) {
        var stepIsValid = true;
        var validator = form.validate();

        $(":input", step).each( function(index) {
            var x = validator.element(this);
            stepIsValid = stepIsValid && (typeof x == 'undefined' || x);
        });
        return stepIsValid;
    },

    progress: function (i, count) {
        $("#progress-complete").width(''+(i/count*100)+'%');
    }
});
```

### Options

- **submitButton**: (required) accepts any supported jQuery selector
- **prevBtnName**: Previous button label. **Default:** Next &gt;
- **nextBtnName**: Next button label. **Default:** &lt; Back
- **prevBtnClass**: Previous button class
- **nextBtnClass**: Next button class
- **buttonTag**: HTML tag used to generate Previous and Next buttons
- **showProgress**: If enabled, shows the steps breadcrumb
- **showStepNo**: If enabled, shows step numbers in breadcrumb
- **validateBeforeNext**: Validation callback before advancing to next step
- **progress**: If defined, fires a callback each time the user advances to next step


### Live examples in jsfiddle

- [example 1](https://jsfiddle.net/artoodetoo/ej13317f/embedded/result/) from Junko: progress as step list, no validation
- [example 2](https://jsfiddle.net/artoodetoo/roct3rcf/embedded/result/) from iFadey: progress like breadcrubms, Validate Engine plugin 
- [example 3](https://jsfiddle.net/artoodetoo/r67b1jkb/embedded/result/) from artoodetoo: progress via callback as color bar, Validation plugin
- [example 4](https://jsfiddle.net/caiorg/qozm39qn/8/embedded/result/) from me: multiple forms support with independent Validation


[1]: http://www.jankoatwarpspeed.com/turn-any-webform-into-a-powerful-wizard-with-jquery-formtowizard-plugin/
[2]: http://www.ifadey.com/2012/06/form-to-wizard-jquery-plugin/
[3]: https://github.com/posabsolute/jQuery-Validation-Engine
[4]: http://jqueryvalidation.org/
[5]: https://github.com/artoodetoo
[6]: https://github.com/artoodetoo/formToWizard