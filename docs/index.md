
# ActionCuts
ActionCuts is an essential tool for any developer making complex and reusable shortcuts. ActionCuts can:

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

Each comment must contain a single line of text in one of two formats: 

\{\{ActionCuts Shortcut:XYZ\}\}

or

\{\{ActionCuts Action:XYZ\}\}

where XYZ is the name of the shortcut or the action block to embed. Consider the screenshot below:

![ActionCuts Embed Comment Format](https://adamtow.github.io/actioncuts/images/actioncuts-embed-comments.png)

The shortcut on the left has three ActionCuts Embed Comments that specify the following shortcuts or actions are to be inserted when processed by ActionCuts:

1. **AC.Header**: A shortcut with the name `AC.Header`.
2. **AC.Application.loop**: A shortcut with the name `AC.Application.loop`.
3. **AC.License**: An action block in the ActionCuts Library called `AC.License`.

****

## Embedding Shortcuts

Follow these steps to embed shortcuts and action blocks into a shortcut:

1. First, add **ActionCuts Embed Comments** in the target shortcut where you want the content to appear. 
2. Open **ActionCuts**.
3. Tap **Embed Shortcuts**.
4. Select the target shortcut.

![Selecting a shortcut containing ActionCuts Embed Comments.](https://adamtow.github.io/actioncuts/images/actioncuts-example-1.png)

ActionCuts will now go through the target shortcut and process any ActionCuts Embed Comments.

![Shortcuts and Action Blocks](https://adamtow.github.io/actioncuts/images/actioncuts-shortcuts-and-actions.png)

In the example given above, ActionCuts will look for two shortcuts with the name `AC.Header` and `AC.Application.loop`. It will also look for an action block called `AC.License` in the ActionCuts Action Block Library. If it finds them on the iOS device, it will insert them exactly where the comment blocks are located.

### Handling Nested Embed Comments

ActionCuts recursively processes the shortcut, meaning if a shortcut or action block being inserted contains ActionCuts Embed Comments, those comments will be processed as well. So, in addition to the three shortcuts and actions listed above, these additional shortcuts were inserted into the target shortcut:

- `AC.Application.about`
- `AC.Application.donate`
- `AC.Application.language`
- `AC.Application.update`

### Handling Missing Shortcuts and Action Blocks

The shortcut `AC.Application.help` could not be found, so the ActionCuts Embed Comment was left as-is. You can run ActionCuts again once you have created a shortcut called `AC.Application.help`, and it will be inserted into the target shortcut.

****

## Extracting Actions

You can extract a block of actions from an existing shortcut and create a new shortcut or save to the ActionCuts Library. This is especially useful when you are writing a long and complicated shortcut. You come up with a great set of actions that you want to re-use in your other shortcuts, but how do you get it out of the shortcut? Traditionally, you have two options, neither of which are ideal:

1. Duplicate the shortcut and remove all actions not pertaining to the one you want to keep. 
2. View the shortcut on another iOS device and manually recreate the shortcut one action at a time. 

With ActionCuts, you only need to:

1. Place two comments before and after the actions you want to save. 
2. Run the Extract Actions command in ActionCuts. 

What used to take minutes or even hours now takes seconds!

![Extracting actions from a shortcut](https://adamtow.github.io/actioncuts/images/actioncuts-extract-example.png)

### ActionCuts Extract Actions Comment Format

In your shortcut, surround the actions you want to extract with two comments:

\{\{ActionCuts Extract:XYZ\}\}

… the actions to extract …

\{\{/ActionCuts Extract:XYZ\}\}

where XYZ is the name of your action block

1. Open **ActionCuts**.
2. Tap **Extract Actions**.
3. Select the shortcut containing the ActionCuts Extract comments. 
4. Save the action block in a new shortcut or into the ActionCuts Library.

### Magic and Named Variables in Action Blocks
In the action blocks that you save or convert into shorcuts, references to any Magic Variables defined outside of the ActionCuts Extract Comments will be broken and labeled in red.

![Magic and Named Variables](https://adamtow.github.io/actioncuts/images/magic-named-variables.png)

If you reference Magic Variables outside of the action blocks, you will have to reconnect the parameters when you insert the action block into the target shortcut.

Named variables are fine — those that are created using the Set Variable action — even though they show up as red. As long as the named variables are defined somewhere else in the target shortcut, the references will be re-associated.

![Fixing Named Variables References](https://adamtow.github.io/actioncuts/images/named-variables-fixed.png)

In the screenshot above, the variable `App (Forever)` was not defined in the Action Block called `AC.Application.loop`, but when it was defined in the target shortcut, the reference to the variable was automatically reconnected.

### Properly Wrapping Action Blocks

It is very important that the ActionCuts Extract Comments are placed correctly around the actions you wish to extract. Consider the following shortcut:

![Oops, this doesn't look right!](https://adamtow.github.io/actioncuts/images/extract-malformed.png)

On the left screenshot, the ending Extract Comment was placed inside of the Repeat action, which itself was inside an If action. The comment should have been placed right outside of the End If action.

When converted into a shortcut, it is readily apparent that the shortcut is malformed. The If action does not have its Otherwise nor End If actions, and the Repeat action does not have its closing End Repeat action.

Placing the starting and end Extract Comments in the wrong place can result in unexpected behavior when running your shortcuts.


****

## Saving Shortcuts and Actions



![Download the processed shortcut back to the iOS device.](https://adamtow.github.io/actioncuts/images/actioncuts-example-2.png)

![ActionCuts Embed Comments have now been replaced with over a hundred plus actions.](https://adamtow.github.io/actioncuts/images/actioncuts-example-3.png)

