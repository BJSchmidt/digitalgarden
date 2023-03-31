---
{"dg-publish":true,"permalink":"/pkm/obsidian/media-extended/","tags":["blogIdea"]}
---


# [Media Extended](https://github.com/aidenlx/media-extended)

The Media Extended plugin for [[PKM/Obsidian/Obsidian\|Obsidian]] lets you play and take notes on videos inside of Obsidian with timestamps!

This works best when combined with the [Templater extension](https://github.com/SilentVoid13/Templater) to allow you to jump to the end of the inserted link.

## Setup

### Timestamp Template:

```
{{TIMESTAMP}}
<%tp.file.cursor(0)%>
```

This inserts the current timestamp, and adds a new templater cursor location.

## Keybindings

### Media Extended: Open Media From Link

`Ctrl-o`

Used to open a video from a link in a new pane

### Media Extended: Get Timestamp From Player

`Ctrl-j`

Insert the Timestamp Template.

### [[Templater\|Templater]]: Jump to Next Cursor Location

`Ctrl-k`

Jump to the end of the timestamp.

## Usage

Open a video from a link with `Ctrl-o`

Insert a bullet into your notes (-)

While watching the video take a new note with `Ctrl-j Ctrl-k`

For example:

[06:13](https://www.youtube.com/watch?v=GQXVWtNkeZw#t=373.881975) This is a note from 6:13 in the video from Bryan Jenks describing this workflow.

# Extendability?

Can this be extended to work with PDFs / Epubs? <https://github.com/caronchen/obsidian-epub-plugin> to take notes with locations from those?
