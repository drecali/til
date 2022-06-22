# Warp: a modern terminal with IDE features.

I recently discovered [Warp](https://www.warp.dev/). It feels like a hybrid between a terminal and an IDE. It has nice modern autocomplete, multi-line editing, and more IDE-esque features. It's free for personal use and will have some paid collaboration features. The Warp team say all the core features you'd expect from a terminal will always be free. It's currently Mac only, so sorry Windows and Linux users 😢

## Features

- One of my favorite features they have is [`workflows`](https://www.commands.dev/). It's like a code snippet with built-in documentation. There's a directory of public workflows, and you can make your own private workflows. I'll put an example below.
- Another nice feature is notifications when a long-running command finishes.

Here's the video from their website that shows a few features in action:

https://user-images.githubusercontent.com/24983797/175027407-d3ebdc14-9cc7-4b66-9517-f654d1d01199.mov

## Workflow example

Here's a custom workflow in the wild. The bottom part is the normal input of the terminal. The gray section is the `workflow`.

  <img width="981" alt="Screen Shot 2022-06-22 at 20 53 34" src="https://user-images.githubusercontent.com/24983797/175024252-279a0333-fdd3-4e05-9c2f-f02b6756a65d.png">

Here is the code responsible for it. It's just a [YAML](https://learnxinyminutes.com/docs/yaml) file!

This is actually my version of an existing workflow. I thought the original could be improved so I did it.

```yaml
---
name: "Find all files in a directory that don't contain a string"
command: 'grep -L "{{string}}" {{directory}}'
tags:
  - search
  - grep
description: "Finds all files in a directory that don't contain a given string."
arguments:
  - name: string
    description: The string to search for
    default_value: ~
  - name: directory
    description: The directory to search. Use '*' for current directory.
    default_value: ~
source_url: "https://stackoverflow.com/questions/1748129/how-do-i-find-files-that-do-not-contain-a-given-string-pattern"
author: ghostdog74
author_url: "https://stackoverflow.com/users/131527/ghostdog74"
shells: []
```

# Resources

- [Warp](https://www.warp.dev/) website
- `workflows` searchable [website](https://www.commands.dev/) and [GitHub repo](https://github.com/warpdotdev/Workflows)
