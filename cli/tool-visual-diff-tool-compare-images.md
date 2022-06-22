# Visual diff tool for comparing images

Computers are much faster than humans at detecting and quantifying subtle differences between images.

## User Story

- I want to quickly and accurately compare 2 images.
- If the images are different, I want to the difference to be quantified and visualized.

## Solution

The [`ODiff`](https://github.com/dmtrKovalenko/odiff) CLI tool from [@dmtrKovalenko](https://github.com/dmtrKovalenko/odiff) is awesome, fast, and easy to use!

ODiff will compare the 2 images pixel-by-pixel and highlight pixels that are have a different color in <span style="color:red;">red</span>. There are configuration options too. See the [repo](https://github.com/dmtrKovalenko/odiff) for details.

❗️ Note that images must be the same size.

## Installation & Use

This should work cross-platform but I only checked on MacOS Monterey, Intel Chip.

```bash
# Installation
npm install odiff-bin

# Use
odiff <IMG1 path> <IMG2 path> <DIFF output path>
```

| `IMG1`                                                                                                          | `IMG2`                                                                                                          | `DIFF`                                                                                                          |
| --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| ![image](https://user-images.githubusercontent.com/24983797/174791065-8e3cfaff-04e3-4b9f-956e-cab74d70f605.png) | ![image](https://user-images.githubusercontent.com/24983797/174791090-00348bf7-1baf-408e-a45d-a3948f7e1934.png) | ![image](https://user-images.githubusercontent.com/24983797/174791125-0aed49c0-5f81-470c-a340-9a7773019744.png) |

## References

The GitHub [repo](https://github.com/dmtrKovalenko/odiff) for the tool.
