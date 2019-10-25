
# ActionCuts
ActionCuts is a powerful tool for embedding shortcuts within shortcuts and extracting actions from existing shortcuts. ActionCuts can:

- Insert complete shortcuts or action blocks inside of other shortcuts.
- Extract action blocks from shortcuts.
- Save expanded shortcuts back to your iOS device.
- Save action blocks in the ActionCuts Action Blocks Library for convenient access to your favorite code snippets.

![ActionCuts Before and After: From 3 to 182 actions in just a few taps!](https://adamtow.github.io/actioncuts/images/actioncuts-before-after.png)

****

## Download
Get the latest version of ActionCuts at RoutineHub.co:

- **[Download ActionCuts &raquo;](https://routinehub.co/shortcut/3761)**

****

## Video Overview
Watch the trailer for [ActionCuts on YouTube](https://youtu.be/VI4oZwKL-28).

## Interface Overview

The following menu is presented by ActionCuts at launch:

- [**Embed Shortcuts**](#embed): Inserts shortcuts within an existing shortcut.
- [**Extract Actions**](#extract): Extract blocks of actions from existing shortcuts.
- [**Actions Library**](#library): Views action blocks that have been saved in ActionCuts.
- **About**: Displays the about dialog with version and build number information.
- **Donate**: Has ActionCuts helped you with your shortcut development? Consider [leaving me a tip](https://www.paypal.me/adamtow)!
- **Help**: Displays help documentation for getting started with ActionCuts.
- **Settings**: Adjust settings used by ActionCuts.
	- **Language**: Change the [language](#localization) used by ActionCuts.
	- **Check for Updates**: Check for updates to ActionCuts on RoutineHub.co.

****

<span id="comment-format"></span>
## ActionCuts Embed Comment Format
ActionCuts works by looking for specially-formatted comments in a shortcut. It replaces these comments with the complete contents of other shortcuts or action blocks from the ActionCuts Library.

Each comment must contain a single line of text in one of two formats: 

`&#123;&#123;ActionCuts Shortcut:XYZ&#125;&#125;`

or

`&#123;&#123;ActionCuts Action:XYZ&#125;&#125;`

where `XYZ` is the name of the shortcut or the action block to embed. Consider the screenshot below:

![ActionCuts Embed Comment Format](https://adamtow.github.io/actioncuts/images/actioncuts-embed-comments.png)

The shortcut on the left has three ActionCuts Embed Comments that specify the following shortcuts or actions are to be inserted when processed by ActionCuts:

1. **AC.Header**: A shortcut with the name `AC.Header`.
2. **AC.Application.loop**: A shortcut with the name `AC.Application.loop`.
3. **AC.License**: An action block in the ActionCuts Library called `AC.License`.

****

<span id="embed"></span>
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

ActionCuts recursively processes the shortcut, meaning if a shortcut or an action block being inserted contains ActionCuts Embed Comments, those comments will be processed as well. So, in addition to the two shortcuts and action listed above, these additional shortcuts were inserted into the target shortcut:

- `AC.Application.about`
- `AC.Application.donate`
- `AC.Application.language`
- `AC.Application.update`

### Handling Missing Shortcuts and Action Blocks

In our example, the shortcut `AC.Application.help` could not be found, so the ActionCuts Embed Comment was left as-is. Once you have created a shortcut called `AC.Application.help`, you can run ActionCuts again, and it will be inserted into the target shortcut.

### Viewing Differences

You can choose to view the differences made by ActionCuts after processing a shortcut and replacing any ActionCuts Embed Comments. ActionCuts uses a [simple diff algorithm](https://johnresig.com/projects/javascript-diff-algorithm/) to show the changes. Text in red represent deletions and text in  green signify additions to the shortcut.

![View the changes made to your shortcuts by ActionCuts](https://adamtow.github.io/actioncuts/images/view-differences.png)

****

<span id="extract"></span>
## Extracting Actions

Imagine you are writing a super long and highly complex shortcut. You come up with a great set of actions that you want to re-use in your other shortcuts, but how do you get it out of the shortcut? Traditionally, you have two options, neither of which are ideal:

1. Duplicate the shortcut and remove all actions not pertaining to the one you want to keep. 
2. View the shortcut on another iOS device and manually recreate the shortcut one action at a time. 

With ActionCuts, you only need to:

1. Place two comments before and after the actions you want to save. 
2. Run the Extract Actions command in ActionCuts. 

What used to take minutes or even hours now takes seconds! With ActionCuts, you can extract entire blocks of actions and place them into a new shortcut or into the ActionCuts Action Blocks Library.

![Extracting actions from a shortcut](https://adamtow.github.io/actioncuts/images/actioncuts-extract-example.png)

### ActionCuts Extract Actions Comment Format

In your shortcut, surround the actions you want to extract with two comments:

`&#123;&#123;ActionCuts Extract:XYZ&#125;&#125;`

… the actions to extract …

`&#123;&#123;/ActionCuts Extract:XYZ&#125;&#125;`

where XYZ is the name of your action block. Note the ending comment has a \/ character preceeding the word `ActionCuts`.

1. Open **ActionCuts**.
2. Tap **Extract Actions**.
3. Select the shortcut containing the ActionCuts Extract Comments. 
4. Save the action block in a new shortcut or into the ActionCuts Action Blocks Library.

### Magic and Named Variables in Action Blocks
In the action blocks that you save or convert into shorcuts, references to any Magic Variables defined outside of the ActionCuts Extract Comments will be broken and labeled in red.

![Magic and Named Variables Broken](https://adamtow.github.io/actioncuts/images/magic-named-variables.png)

If you reference Magic Variables outside of the action blocks, you will have to reconnect the parameters when you insert the action block into the target shortcut.

Named variables, on the other hand, are fine — those that are created using the Set Variable action — even though they show up as red. As long as the named variables are defined somewhere else in the target shortcut, the references will be re-associated.

![Fixing Named Variables References](https://adamtow.github.io/actioncuts/images/named-variables-fixed.png)

In the screenshot above, the variable `App (Forever)` was not defined in the Action Block called `AC.Application.loop`, but when it was defined in the target shortcut, the reference to the variable was automatically re-established.

### Properly Wrapping Action Blocks

It is very important that the ActionCuts Extract Comments are placed correctly around the actions you wish to extract. Consider the following shortcut:

![This results in a malformed shortcut.](https://adamtow.github.io/actioncuts/images/extract-malformed.png)

On the left screenshot, the ending Extract Comment was placed inside the Repeat action, which itself was inside an If action. The comment should have been placed right outside the End If action.

When converted into a shortcut, it is readily apparent that the shortcut is malformed. The If action does not have its Otherwise nor End If actions, and the Repeat action does not have its closing End Repeat action.

Placing the starting and end Extract Comments in the wrong place can result in unexpected behavior when running your shortcuts.

****

## Action Blocks Library

Saved action blocks are available for viewing in the Action Blocks Library section of ActionCuts. Tapping on the Actions Library menu item will display all saved action blocks. Tap on an action block to reveal the following menu:

- **Download as Shortcut**: Wraps the action block in a shortcut shell and uploads it to iCloud so it can be downloaded to your iOS device.
- **Copy ActionCuts Comment**: Copies the ActionCuts Extract Comment for the specified action block. You can paste this in a comment in a shortcut. Running the Embed Shortcuts command will insert the action block into the target shortcut.
- **View Action Block**: Displays a text view of the action block in [plist format](https://en.wikipedia.org/wiki/Property_list).
- **Delete Action**: Delete the action block. This operation cannot be undone.
- **Back to Action Library**: Returns to the list of action blocks.
- **Back to ActionCuts Home**: Returns to the ActionCuts Home screen.

![ActionCuts Action Blocks Library.](https://adamtow.github.io/actioncuts/images/actions-library.png)

****

<span id="save"></span>
## Saving Shortcuts and Actions

When you embed shortcuts and extract action blocks, ActioCuts will give you the opportunity to create a new shortcut. Choosing this option will upload the shortcut to iCloud Drive and provide you a link to the new shortcut.

![Download the processed shortcut back to the iOS device.](https://adamtow.github.io/actioncuts/images/actioncuts-example-2.png)

![ActionCuts Embed Comments have now been replaced with over a hundred plus actions.](https://adamtow.github.io/actioncuts/images/actioncuts-example-3.png)

> **NOTE**: Shortcuts downloaded to your device via ActionCuts have the string `.shortcut` appended to the end of the filename. This is unavoidable at the moment, but you can always update the name of the shortcut after downloading.

****

<span id="localization"></span>
## Localization

ActionCuts is fully localized for the English language, and it has been auto-translated into many other languages. If you would like to contribute and a more accurate localization file for ActionCuts, please visit [ActionCuts' localization page here](https://github.com/adamtow/actioncuts/tree/master/localization).

****

<span id="acknowledgements"></span> 
## Acknowledgements

ActionCuts was inspired by [CopyPaste Actions](https://routinehub.co/shortcut/500) by /u/schl3ck and [MergeCuts](https://routinehub.co/shortcut/3724) by /u/ROPit.

****

<span id="license"></span>
## License

Copyright © 2019 Adam Tow • tow.com • @atow

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
