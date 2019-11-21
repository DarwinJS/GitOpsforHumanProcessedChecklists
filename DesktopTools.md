# Markdown Checklists Methods and Tools

## Typora For Checklists

### Typora Features That Make Markdown Checklists more Workable

Typora is a markdown editor that unifies the markdown editing experience into one pain that both edits and renders markdown.  Editing is accomplished via inserting markdown (which is immediately rendered) or through menu commands like a word processor like Microsoft Word.

1. Multiplatform for DevOps teams - Windows, Mac, Linux. (electron based)
2. Free.
3. Creates **standard** markdown - renders properly in code editors and source control web UIs.
4. **DISTINGUISHING FEATURE:** Visual editing that takes markdown directly (and converts it on the fly) - all in one pane.
5. Menu, Right-click and familiar hotkeys for common word processing formatting like Bolding (that creates native MD)
6. **DISTINGUISHING FEATURE:**  Table of Contents builder.
7. **DISTINGUISHING FEATURE:** Outline navigation mode makes complex checklists easier to construct and navigate. (once you've installed Typora, view this very document in it to see how helpful this is)
8. **DISTINGUISHING FEATURE:** Excellent table support.
9. Strikethrough hotkeys for marking items done (CTRL-SHIFT-5).
10. **SERIOUSLY DISTINGUISHING FEATURE:** Ability to paste graphics and relocate the graphic into the repo folder without leaving the editor.  Usable for creating checklists with screenshot instructions and completing checklists with recorded screenshots for completion evidence.
11. Source control / Code editor agnostic - works as a reader and writer and regardless of source control technology or code editor in use by a team or individual. (although you must update the path to be relative, not fully resolved - easily done in the editor)
12. Replaces currently selected text with a paste operation (easy replacement / update of stamps)
13. Undo functionality - easy undo of stamping.
14. Spellcheck !

### CopyQ Features That Make Markdown Checklists More Workable

If you exclusively use the built in Strikethrough hotkey of Typora to mark items "Done", then you would not need to add CopyQ to the solution.  If you want more flexibility with Done stamping, other kinds of stamps, and standard, formatted markdown inserting, CopyQ rocks.

CopyQ is a multiplatform clipboard management tool.  It can insert standard bits of text. Since Typora supports direct input of markdown - clips you build in CopyQ can include straight markdown for formatting.  In addition, it can insert a formatted current date time stamp.  It can controlled with user defined hotkeys.

While CopyQ is presented here as working with Typora, the markdown text inserts you build with it would insert into any Markdown editor - so just this part of the solution can be adopted if desired.

1. Multiplatform for DevOps teams - Windows, Mac, Linux. (QT Based)
2. Free.
3. Supports text insertion macros into anything - including Typora.
4. Since Typora receives markdown directly, the text insertion can include raw markdown for formatting.
5. Supports time date stamp inserting - also with formatting of the date and of the surrounding markdown.
6. **DISTINGUISHING FEATURE:** You can export and import your commands for sharing on a team.

## Installing Typora and CopyQ

### Windows

```
#Idempotently installs chocolatey if not present
If (!(Test-Path env:chocolateyinstall)) {iwr https://chocolatey.org/install.ps1 -UseBasicParsing | iex} ; chocolatey install -y typora copyq
```

### Mac

```
brew cask install typora copyq
```

#### Installation on Linux (Ubuntu)

Typora is only tested on Ubuntu - (In private repo that requires config): http://support.typora.io/Typora-on-Linux/

CopyQ (In public package repos it is published as "CopyQ"): https://copyq.readthedocs.io/en/latest/installation.html

## To Insert Done Date and Time Multiplatform

### Configure CopyQ with TODO and DONE Stamps

The code for the below stamps as well as several others can be imported into CopyQ using this CopyQ settings import file: [copyq-command-import.ini](copyq-command-import.ini)

#### CopyQ Code for "DONE" with Time Stamp

**Note:** The color span tags will not render everywhere (they do in Typora), by adding the square brackets and bold, they standout in renderings that don't support CSS styling.

Create a new command with a hotkey with this code (customize date and text as you desire):

```copyq: 
copyq: 
// http://doc.qt.io/qt-5/qdatetime.html#toString
var format = 'MM/dd @ hh:mm'
var dateTime = dateString(format)
copy('<span style="background-color:lightgreen;border: 1px">**[DONE ' + dateTime + ']**</span> ')
copySelection(dateTime)
paste()
```

#### CopyQ Code for "TODO" Stamp

Create a new command with a hotkey with this code.

```copyq: 
copyq: 
var todotag = '<span style="background-color:lightblue;border: 1px">**[TODO]**</span> ' 
copy(todotag)
copySelection(todotag)
paste()
```

#### Other Stamp Ideas

- [SKIPPED: _DATE_ _REASON_]
- [RECORD RESULT HERE]
- List of CSS colors to use in stamps: https://www.quackit.com/css/css_color_codes.cfm

#### More Docs on Formatting and Commands in CopyQ

CopyQ could actually be used to do things that Tyopora currently does not - for example, change the color of selected text.  You could even get fancy and try to get your code to find the start of the current line - minus the bullet - before inserting or search for the square brackets to allow replacing of one stamp with another.

Docs on CopyQ: https://copyq.readthedocs.io/en/latest/command-examples.html?highlight=paste%20specific%20text#paste-current-date-and-time

QT Date Stamp Formatting: https://doc.qt.io/qt-5/qdatetime.html#toString

## Screenshot of the Above Rendered in Typora

Since Typora itself is what you would edit with, a visual preview is helpful if you are viewing this in another rendering engine:

![typorapreview.png](typorapreview.png)

## Appendix: Architecture Heuristics: Requirements, Constraints, Desirements, Serendipities, Applicability, Limitations and Alternatives

The following list demonstrates the Architectural thrust of the solution.  It can help you discover problems you don't know you'll have yet and whether your needs and goals for operational checklists (or something similar) have reasonable alignment with the ones used to decide on the elements of this solution.

- **Requirement: (Satisfied)** Multiplatform for DevOps teams who use a mix of Mac and Windows.
- **Requirement: (Satisfied)** Leverages free software.
- **Requirement: (Satisfied)** Markdown checkboxes do not work in combination with Markdown numbered bullets - so the entire solution must support another method of done marking.
- **Requirement: (Satisfied)** Current date and time inserts for "Done" stamping using a hotkey.
- **Requirement: (Satisfied)** Markdown formatting of hotkey based text inserts.
- **Requirement: (Satisfied)** Not web based (or at least not JIRA based) because it is easy to loose track of the window and there is the risk of losing progress if I don't save and re-edit regularly (something that increases cognitive load during the already mentally intensive execution of an operational checklist).
- **Requirement: (Satisfied)** Code editor and source control manager agnostic - does not require team members to standardize their editor or various teams to be on the same source control.
- **Requirement: (Satisfied)** standard, plain vanilla flavored markdown should be the primary mark up.
- **Desirement: (Satisfied)** Proper handling of pasting graphics and locating them next to source files.  Graphics dramatically enhance instructions and allow screen capture based recording of results.
- **Desirement: (Satisfied)** Uses visual editing - not the dual pane editing and rendering approach used by most markdown tools.
- **Desirement: (Satisfied)** Table support for long lists of parameters.
- **Desirement: (Satisfied)** CSS rendering for visually distinguished tags.
- **Serendipity: (Discovered)** Outline navigation pane for easier navigation of complex checklists.
- **Serendipity: (Discovered)** Replace selected text with paste, Undo control key.
- **Serendipity: (Discovered)** Decent spell check.
- **Serendipity: (Discovered)** Autosave functionality (loosing checklist progress is jarring during change events).
- **Serendipity: (Discovered)** support for standard formatting through well-known hotkeys, menu items and right-click menus (like a word processor rather than a code editor).
- **Serendipity: (Discovered)** export of command configuration from hotkey utility for easy sharing of extended stamps and text formatting.
- **Serendipity: (Discovered)** all tools are already in the standard package repositories for Windows (Chocolatey) and Mac (Brew).