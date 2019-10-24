
# ActionCuts
ActionCuts is an essential tool for developers making complex and reusable shortcuts. ActionCuts can:

- Insert complete shortcuts or action blocks inside of other shortcuts.
- Extract action blocks from shortcuts.
- Save expanded shortcuts back to your iOS device.
- Save action blocks in the ActionCuts Library for convenient access to your favorite shortcut code snippets.

Developing shortcuts has gotten a lot easier with ActionCuts!

![ActionCuts Before and After: From 3 to 182 actions!](https://adamtow.github.io/actioncuts/images/actioncuts-before-after.png)

****

## Download
Get the latest version of ActionCuts at RoutineHub.co:

- **[Download ActionCuts &raquo;](https://routinehub.co/shortcut/3761)**

****

## ActionCuts Embed Comment Format
ActionCuts works by looking for specially-formatted comments in a shortcut. It replaces the comment with the complete contents of another shortcut or an action block from the ActionCuts Library.

Each comment contains a single line of text:

`{{ActionCuts Shortcut:XYZ}}`

or

`{{ActionCuts Action:XYZ}}`

where XYZ is the name of the shortcut or action block to embed. Consider the screenshot below:

![ActionCuts Embed Comment Format](https://adamtow.github.io/actioncuts/images/actioncuts-embed-comments.png)

The shortcut on the left has three ActionCuts Embed Comments that specify the following shortcuts or actions are to be inserted when processed by ActionCuts:

1. **AC.Header**: A shortcut with the name `AC.Header`.
2. **AC.Application.loop**: A shortcut with the name `AC.Application.loop`.
3. **AC.License**: An action block with the name `AC.License`.

****

## Embedding Shortcuts

Follow these steps to embed shortcuts and action blocks into a shortcut:

1. Add **ActionCuts Embed Comments** to the target shortcut.
2. Open **ActionCuts**.
3. Tap **Embed Shortcuts**.
4. Select the target shortcut.

![Selecting a shortcut containing ActionCuts Embed Comments.](https://adamtow.github.io/actioncuts/images/actioncuts-example-1.png)

Any ActionCuts Embed Comments in the shortcut will be processed and replaced by the referenced shortcut or action block, provided they exist on the iOS device.

![Shortcuts and Action Blocks](https://adamtow.github.io/actioncuts/images/actioncuts-shortcuts-and-actions.png)

In the example given above, ActionCuts will look for two shortcuts with the name `AC.Header` and `AC.Application.loop` and will look for an action block called `AC.License` in the ActionCuts Action Block Library. If it finds them, it will insert them exactly where the comment blocks are located.

### ActionCuts Knows Recursion

ActionCuts recursively processes the shortcut, meaning if a shortcut that is being inserted into a shortcut contains ActionCuts Embed Comments, those comments will be processed as well. So, in addition to the three shortcuts and actions listed above, these additional shortcuts were inserted into the target shortcut:

- `AC.Application.about`
- `AC.Application.donate`
- `AC.Application.language`
- `AC.Application.update`

### Handling Missing Shortcuts and Action Blocks

The shortcut `AC.Application.help` could not be found, so the ActionCuts Embed Comment was left behind. You can run ActionCuts again once you have created a shortcut called `AC.Application.help` and it will be inserted into the target shortcut.

****

## Extracting Actions

You can extract a block of actions from an existing shortcut and create a new shortcut or save to the ActionCuts Library. This is espe

![Extracting actions from a shortcut](https://adamtow.github.io/actioncuts/images/actioncuts-extract-example.png)

1. In your shortcut, surround the actions you want to extract with two comments:\
\
`{{ActionCuts Extract:XYZ}}`\
\
… the actions to extract …\
\
`{{/ActionCuts Extract:XYZ}}`\
\
where XYZ is the name of your action block\
\
\

2. Open **ActionCuts**.
3. Tap **Extract Actions**.
4. Select the shortcut from Step 1.
5. Save the action block in a new shortcut or into the ActionCuts Library.


****

## Saving Shortcuts and Actions



![Download the processed shortcut back to the iOS device.](https://adamtow.github.io/actioncuts/images/actioncuts-example-2.png)

![ActionCuts Embed Comments have now been replaced with over a hundred plus actions.](https://adamtow.github.io/actioncuts/images/actioncuts-example-3.png)

