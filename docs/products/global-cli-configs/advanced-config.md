# Advanced config

## Global config

You can configure how the Grid CLI behaves by changing the global config file at:

* `~/.grid/settings.json`

```javascript
{
    "debug": false,
    "ignore_warnings": true
}
```

## debug

If `true` the CLI will print additional logging. This is useful for debugging a particular issue and giving feedback.

## ignore\_warnings

When set to `true`, this will ignore all warnings that the CLI makes. This is useful in case you are trying to avoid a repetitive warning from Grid.

{% hint style="info" %}
The Grid CLI warnings are really useful to prevent mistakes. Only change this value if you really know what you are doing.
{% endhint %}

