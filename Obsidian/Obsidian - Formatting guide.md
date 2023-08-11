Type: #Obsidian #styleguide

## General markdown formatting
- basic - https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax
- advanced - https://help.obsidian.md/Editing+and+formatting/Advanced+formatting+syntax
- Obsidian specific:

| Syntax      | Description                                                                                  |
| ----------- | -------------------------------------------------------------------------------------------- |
| `[[ ]]`     | [Internal links](https://help.obsidian.md/Linking+notes+and+files/Internal+links)            |
| `![[ ]]`    | [Embedding files](https://help.obsidian.md/Linking+notes+and+files/Embedding+files)          |
| `%%`        | [Comments](https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax#Comments) |
| `> [!note]` | [Callouts](https://help.obsidian.md/Editing+and+formatting/Callouts)                         |

## Callouts
Use to highlight info
- general format:
```
> [!info] <insert title here if wanted>
> Here's a callout block. 
> It supports **Markdown**, [[Internal link|Wikilinks]], and [[Embed files|embeds]]! 
```

> [!info]+ insert title here if wanted
> Here's a callout block. 
> It supports **Markdown**, [[Internal link|Wikilinks]], and [[Embed files|embeds]]! 

- You can make a callout foldable by adding a plus (+) or a minus (-) directly after the type identifier. (+) = default expand
- can be nested
- 
### Callout types
- `[!note]`
- `[!abstract]` - also summary, tldr
- `[!info]`
- `[!tip]` - also hint, important
- `[!success]` - also check, done
- `[!question]` - also help, faq
-  `[!failure]` - also fail, missing
-  `[!danger]` - also error 
-  `[!bug]` 
-  `[!example]` 
-  `[!quote]` - also cite 

### Custom callouts

```css
.callout[data-callout="custom-question-type"] {
    --callout-color: 0, 0, 0;
    --callout-icon: lucide-alert-circle;
}
```
