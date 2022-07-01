# RegEx is awesome - online RegEx playgrounds and cheatsheets

## What's a RegEx?

[Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) are like an overpowered `Cmd/Ctrl + F` that can match to a very specific bit of text. Like CRISPR for matching `strings`.

When evaluating a string of any length, it can detect things like:

- very specific combination of numbers and/or letters and/or special characters. This one is super practical for detecting:
  - emails
  - phone numbers
  - postal codes
  - IP addresses
- all words with an upper case letter.
- all words using a certain set of characters (like all Korean/한글 words)
- all words of a certain size
- all instances of a special character
- `tabs`, `spaces`, or `linebreak` characters.

There are different versions used by different programming languages. I mostly use JavaScript so that's my bias for this article.

## How do you harness their power?

It's really powerful but not the most fun to learn or use with traditional resources. Its very powerful but very complex. It's not something most devs use frequently and it would take too long to study all all the components of RegEx.

<details>
  <summary> 💥 Bonus: See how to use RegEx within VS Code</summary>
💥 Bonus: You can use RegEx within VS Code and likely other code editors to boost the power of the `Find and Replace` feature. I wish Chrome natively supported this.

![image](https://user-images.githubusercontent.com/24983797/176911212-e01416c9-4f3c-4ab5-9d83-9712ca6d2588.png)

</details>

## Learn it on your own terms

Thankfully, some very nice and passionate devs built quick reference playground sites that have concise cheatsheets, explain how your custom RegEx works, and allow you to test it with your own custom text strings.

`RegExr` is a tool I discovered early in my studies and I stuck with it because I adore it and haven't ran into its limitations. It's minimalist but has concise explanations and examples too. The tooltips are nice too.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/24983797/176908996-9a076035-05b9-45ad-9783-3a56371f57ed.png">

There are other tools too. These are linked on the MDN page and I'll be trying them soon.

- [Regex Tester](https://extendsclass.com/regex-tester.html) by ExtendsClass
  - I'm a big fan of their visualization.
    <img width="335" alt="image" src="https://user-images.githubusercontent.com/24983797/176909738-c7f732c2-3c8a-44fb-ab27-46b19d380199.png">
- [RegexLearn Playground](https://regexlearn.com/playground)
- [regex101](https://regex101.com/) has nice unit testing interface built-in.
