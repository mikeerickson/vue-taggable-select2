# vue-taggable-select2

A Vue component that makes long, unwieldy select boxes user friendly.

[Check out a demo here](https://codesandbox.io/s/18jz68zn77)

## Note

This component has been forked from [vue-taggable-select](https://github.com/robrogers3/vue-taggable-select) as it has gone cold and I had some issues that needing fixing

## What it Does

vue-taggable-select2 provides an elegant, user-friendly component to replace long, unwieldy multi select elements. Great for users. Simple for developers.

## Simple API

```html
<vue-taggable-select2 :taggable="true" v-model="sport" :options="['baseball','football','basketball','hocke']"></vue-taggable-select2>
```

<img style="width: 400px" src="https://raw.githubusercontent.com/mikeerickson/vue-taggable-select2/master/vue-taggable-select2.png">

## What It Does Not Do

Currently, does not provide a simple select component (but we are planning to implement). In the meantime, try out this component!

[Vue Single Select](https://www.npmjs.com/package/vue-single-select)

No ajax loading.

## Usage

### Install and Use Via CDN

```html
<div id="app">
    <lable>Choose a sport!</lable>
    <vue-taggable-select2 v-model="sport" :options="sports"></vue-taggable-select2>
</div>
```

```html
<script src="https://unpkg.com/vue@latest"></script>
<script src="https://unpkg.com/vue-taggable-select2@latest"></script>
<script>
    new Vue({
        el: "#app",
        data: {
            sport: ["baseball"],
            sports: ["baseball", "football", "basketball", "hockey"],
        },
    })
</script>
```

### Install Via NPM

```bash
> npm i @codedungeon/vue-taggable-select2
```

### Register it

In your component:

```javascript
import VueTaggableSelect2 from "vue-taggable-select2"
export default {
    components: {
        VueTaggableSelect2,
    },
    //...
}
```

Globally:

```javascript
import VueTaggableSelect2 from "vue-taggable-select2"
Vue.component("vue-taggable-select2", VueTaggableSelect2)
```

### Use It

```html
<vue-taggable-select2 make-it-taggable="good!" :taggable="true" v-model="sport" :options="['baseball','football','basketball','hockey']" :required="true"></vue-taggable-select2>
```

### Use It Again

```html
<vue-taggable-select2
    name="maybe"
    placeholder="pick a post"
    you-want-to-select-a-post="ok"
    v-model="post"
    out-of-all-these-posts="makes sense"
    :options="posts"
    a-post-has-an-id="good for search and display"
    option-key="id"
    the-post-has-a-title="make sure to show these"
    option-label="title"
></vue-taggable-select2>
```

### Use It Again

```html
<vue-taggable-select2
    you-want-to-select-a-reply="yes"
    v-model="reply"
    out-of-all-these-replies="yep"
    :options="replies"
    a-reply-only-has-a-reply="sounds about right"
    option-label="reply"
    seed-an-initial-value="what's seed mean?"
    initial="seed me"
    you-only-want-20-options-to-show="is 20 enough?"
    :max-results="20"
></vue-taggable-select2>
```

### Dont like the Styling?

You can override some of it. Like so:

```html
<vue-taggable-select2
    id="selected-reply"
    name="a_reply"
    option-label="reply"
    v-model="reply"
    :options="replies"
    you-like-huge-dropdowns="1000px is long!"
    max-height="1000px"
    :classes='{
            icons: "icons"
            active: "active",
            wrapper: "multi-select-wrapper",
            searchWrapper: "search-wrapper",
            searchInput: "search-input",
            pill: "pill",
            required: "required",
            dropdown: "dropdown"
        }'
></vue-taggable-select2>
```

Then all you need to do is provide some class definitions like so:

```css
.active {
    background-color: pink;
}
.multi-select-wrapper {
    display: block;
    font-size: 16px;
}
.search-input {
    color: black;
}
.pill {
    padding: 0.5em;
}
```

... and so on.

**Note: Bootstrap 3 Users May want to increase the size of the icons.**

If so do this:

```css
.icons svg {
    height: 1em;
    width: 1em;
}
```

## Why vue-taggable-select2 is better

1.  It handles custom label/value props for displaying options.

    Other select components require you to conform to their format. Which often means data wrangling.

2.  It's easier on the DOM.

    Other components will load up all the options available in the select element. This can be heavy. vue-taggable-select2 makes an executive decision that you probably will not want to scroll more than N options before you want to narrow things down a bit. You can change this, but the default is 30.

3.  Snappy Event Handling

    -   up and down arrows for selecting options
    -   enter to select first match
    -   remembers selection on change
    -   hit the escape key to, well, escape
    -   hit delete to remove the last selection

4.  Lightweight

    -   Why are the other packages so big and actually have dependencies?

5.  It works for regular 'POST backs' to the server.

    If you are doing a regular post or just gathering the form data you don't need to do anything extra to provide a name and value for the selected option.

## Available Props

```javascript
props: {
    // This corresponds to v-model
    value: {
        type: [String, Array],
        required: true
    },
    taggable: {
        type: Boolean,
        default: () => false
    },
    // Use classes to override the look and feel
    // Provide these EIGHT classes.
    classes: {
        type: Object,
        default: () => {
            return {
                icons: 'icons',
                active: 'active',
                wrapper: "multi-select-wrapper",
                searchWrapper: "search-wrapper",
                searchInput: "search-input",
                pill: "pill",
                required: "required",
                dropdown: "dropdown"
            };
        }
    },
    // Give your input a name
    // Good for posting forms
    name: {
        type: String,
        default: () => ""
    },
    // Your list of things for the select
    options: {
        type: Array,
        default: () => []
    },
    // Tells vue-taggable-select2 what key to use
    // for generating option labels
    optionLabel: {
        type: String,
        default: () => null
    },
    // Tells vue-taggable-select2 the value
    // you want populated in the select for the
    // input
    optionKey: {
        type: String,
        default: () => null
    },
    // Give your input an html element id
    placeholder: {
        type: String,
        default: () => "Search Here"
    },
    maxHeight: {
        type: String,
        default: () => "220px",
    },
    //Give the input an id
    inputId: {
        type: String,
        default: () => "multi-select",
    },
    // Seed search text with initial value
    initial: {
        type: String,
        default: () => null
    },
    // Make it required
    required: {
        type: Boolean,
        default: () => false
    },
    // Max number of results to show.
    maxResults: {
        type: Number,
        default: () => 256
    },
    //Meh
    tabindex: {
        type: String,
        default: () => {
            return "";
        }
    },
    // Remove previously selected options
    // via the delete key
    keyboardDelete: {
        type: Boolean,
        default: () => {
            return true;
        }
    },
    // Tell vue-taggable-select2 how to display
    // selected options
    getOptionDescription: {
        type: Function,
        default(option) {
            if (this.optionKey && this.optionLabel) {
                return option[this.optionKey] + " " + option[this.optionLabel];
            }
            if (this.optionLabel) {
                return option[this.optionLabel];
            }
            if (this.optionKey) {
                return option[this.optionKey];
            }
            return option;
        }
    },
    // Use this to tell vue-taggable-select2
    // the values are for doing a submit
    getOptionValue: {
        type: Function,
        default(option) {
            if (this.optionKey) {
                return option[this.optionKey];
            }

            if (this.optionLabel) {
                return option[this.optionLabel];
            }

            return option;
        }
    }
},
```
