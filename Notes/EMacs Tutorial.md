---
tags:
  - note
link: https://www.youtube.com/watch?v=48JlgiBpw_I
---
# `= this.file.name `
---

### The User Interface
---

Emacs has a menu and tool bar like many conventional graphical programs. They can be useful at first to learn the functionality that is available, but most developers don't use them for long!

```ad-tip
Note that the menu bar actually is present in the terminal version of Emacs
```

If you're coming from another IDE or editor, you might expect to see a file tree on the left side of the window. This isn't provided by Emacs by default, but it's easy to add through community packages. There are other ways to show files in Emacs that are arguably even better than a window tree!

`C-v`
		Move forward one screen-full
`M-v`
		Move backward one screen-full
`C-l`
		Clear screen and redisplay all the text,
		 moving the text around the cursor
		 to the center of the screen.
		 (That's `CONTROL-L`, not `CONTROL-1`.)

### Windows and Frames
---

The concept of a "window" is different in Emacs than what you probably know from using graphical computing environments. In modern desktop environments, a window is a graphical interface of a program which is managed by the window manager of the desktop environment, usually with buttons or close or minimise it.

In Emacs, a window is more like a "pane" in the desktop window *of* Emacs. A window in Emacs always displays a **buffer**. Windows can also be split in arbitrary ways, both horizontally and vertically, so that you can create whatever window layout you like. Each of  these windows can show different buffers or even the same buffer!

What you think of as a window in typical desktop environments, Emacs calls a "frame"!

```
Frames that can be split -> Multiple buffers with their own history
```

Emacs can display multiple frames at the same time. These frames all share the *same internal state and buffers*. Some people use more than one frame, others use many frames. It all depends on how you prefer to use Emacs.

### Buffers
---

A buffer holds text and other information that is usually displayed in a window.

However, there are many types of special buffers that are used only for displaying temporary information or user interface elements! The Magit package provides an excellent interface for Git inside of a custom Emacs buffer.

Some important buffers you will definitely see when you use Emacs:

- `*scratch*` Essentially a blank sheet of paper for taking notes, writing temporary Emacs Lisp expressions, or whatever you would like.
- `*Messages*` This contains log messages and all the text that gets written to the echo area at the bottom of the screen.
- `*Warnings*` A list of potential errors

A buffer can be used as a custom user-interface for any task that you would like to do. With it's own hotkeys and implementations.







---
Created: May 18, 2024
Last Modified: `= this.file.mtime`
