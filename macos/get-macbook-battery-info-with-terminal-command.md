# Get MacBook battery info with terminal command

It's possible to access MacOS battery information from the terminal. The following command will output the battery's:

- design capacity - its maximum capacity when new
- maximum capacity - its current maximum capacity (which is usually lower than the design capacity and will decrease a small amount every battery cycle)
- the current capacity - the current amount of charge remaining in the battery (this is the amount shown in the battery icon in the menu bar)

```bash
ioreg -l |grep -e '"DesignCapacity" =' -e '"AppleRawMaxCapacity" =' -e '"AppleRawCurrentCapacity" ='
```

<details>
    <summary>Terminal command explained</summary>

### `ioreg -l`

- `ioreg`: This is a command-line utility in macOS that displays the I/O Kit registry, which contains data about all the hardware and devices connected to the system.
- `-l`: This option requests a detailed (verbose) listing of the properties for each object in the I/O Kit registry. This is required to get the battery information.

### `| grep -e`

- `|`: This is a pipe operator, used to pass the output of one command as input to another command. In this case, the entire verbose listing of the I/O Kit registry is passed to the `grep` command.
- `grep`: This command searches for specific patterns within the input text and outputs the line(s) containing the pattern. It's similar to <kbd>Ctrl/Cmd</kbd> + <kbd>F</kbd> in a text editor.
- `-e`: This option allows specifying multiple patterns to search for. Each pattern is specified after `-e`.

### `'"DesignCapacity" =' -e '"AppleRawMaxCapacity" =' -e '"AppleRawCurrentCapacity" ='`

These are the patterns we are searching for in the output of `ioreg -l`. Each pattern corresponds to battery property. Notice the patterns are separated by `-e` and each pattern is enclosed in double quotes and followed by an equal sign and a space. This is to ensure that we only match the exact property names and not other text that might contain similar words.

💡 `ioreg -l` contains a LOT of info. It's fun to `grep` around for other patterns and see what you can uncover. Have fun!

</details>
<br>

The output will look something like this:

```bash
    | |   |       |   |       "AppleRawCurrentCapacity" = 6367
    | |   |       |   |       "DesignCapacity" = 6249
    | |   |       |   |       "AppleRawMaxCapacity" = 6406
```

In this case, the MacBook is very new so `AppleRawMaxCapacity` and `AppleRawCurrentCapacity` are higher than `DesignCapacity`. This is normal for new batteries and is a result of the manfuacturing process. Manufacturers aim to deliver batteries with the design capacity but manufacturing processes are imprecise so real capacity can be a bit higher or lower. If they produce batteries with a capacity higher than the design capacity they can ensure that **all** customers will receive a battery with **at least** the design capacity, even though some will get a bit of free _bonus_ battery capacity.

# References

- [Apple Support - About Mac notebook batteries](https://support.apple.com/en-us/HT201585)
- [Apple Support - How to check the battery health of your MacBook](https://support.apple.com/en-us/HT211094)
- [Reddit thread](https://www.reddit.com/r/MacOS/comments/17rg0sf/is_coconut_battery_unreliable/?rdt=52398)
