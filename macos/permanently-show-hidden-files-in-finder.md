# Permanently show hidden files in Finder

If a file or folder name starts with a `.` (dot), it is considered hidden. Because they start with a dot, they are also known as `dotfiles`.

On MacOS, hidden files are not shown in Finder by default.

There is no menu option to show hidden files in Finder. Why? Because Apple thinks you can't handle messing with hidden files, and Apple knows better than you. Even if you're a developer. 🤷‍♂ ️

There **is** a keyboard shortcut to do this temporarily: <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>.</kbd>. This toggles hidden files on and off. This is kind of annoying if you're a developer and you want hidden files shown by default in Finder.

To permanently show hidden files in Finder, you can run the following command in the terminal:

```bash
defaults write com.apple.finder AppleShowAllFiles TRUE

# If you also want to restart all open Finder windows too:
defaults write com.apple.finder AppleShowAllFiles TRUE ; killall Finder
```

To hide hidden files again, run the following command:

```bash
defaults write com.apple.finder AppleShowAllFiles FALSE

# If you also want to restart all open Finder windows too:
defaults write com.apple.finder AppleShowAllFiles FALSE ; killall Finder
```

This will show hidden files in Finder. You can toggle this setting by changing `TRUE` to `FALSE` and vice versa.

## References

- [How to view files on your Mac that are normally invisible? - FAQ 1792 - GraphPad](https://www.graphpad.com/support/faq/how-to-view-files-on-your-mac-that-are-normally-invisible/#:~:text=Method%203.%20Use%20Terminal)
