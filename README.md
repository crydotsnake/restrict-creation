# Flowpack.RestrictCreation

Imagine the situation: you have a website with 'English (US)', 'English (UK)' and 'German' content dimensions present.

Now you never want editors to create new nodes directly in 'English (UK)', without first creating them in 'English (US)' and almost never in 'German', but some really rare cases.

This package provides an option to enforce these kind of constraints:

![restrictcreation](https://user-images.githubusercontent.com/837032/47265437-80bfcc80-d530-11e8-8e86-d469e2fb7ba7.gif)

## Getting started:

1. `composer require 'flowpack/restrictcreation'`
2. Configure your dimensions in Settings.yaml, e.g. like this:

```
Neos:
  ContentRepository:
    contentDimensions:
      language:
        presets:
          en_US:
            label: 'English (US)'
            values:
              - en_US
            uriSegment: en
          en_UK:
            label: 'English (UK)'
            values:
              - en_UK
              - en_US
            uriSegment: uk
            restrictCreation:
              mode: disallow
              originPreset: en_US
          de:
            label: German
            values:
              - de
            uriSegment: de
            restrictCreation:
              mode: warn
              originPreset: en_US
```

`mode: warn` would only give a warning about creating a node in a possible wrong dimensiong.
`mode: disallow` would completely forbid creating new nodes in a certain dimension.

## Acknowledgments

The initial development of this package is sponsored by [web&co](http://webundco.com/).
