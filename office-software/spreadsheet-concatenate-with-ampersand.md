# `[Spreadsheet]` - Concatenate with `&` operator

In Spreadsheet software like Google Sheets or Microsoft Office, the `&` operator does 2 beautiful things:

- Converts the output of the 2 elements on either side of it as `strings`
- Joins the `string` outputs

```sh
= 0 & 5 # 05
= 'con' & 'cat' # concat
```

It's especially useful for summary cells when you want to show 2 values in the same cell or format a value in an uncommon way that may not be built in to the spreadsheet software (or you don't feel like finding it). For example:

```sh
= SUM(A1:A10) & 'mL' # 500mL
= 'Total: ' & SUM(A1:A10) & ` | Avg: ` & AVERAGE(A1:A10) # Total: 500 | Avg: 250
```

## Resources

- [Excel Operators](<https://excelx.com/formula/operators/#:~:text=%2C%3DA2%2DA1-,Concatenation%20Operator,result%20will%20be%20a%20string.&text=We%20can%20use%20%26(Ampersand)%20Operator%20to%20concatenate%20two%20strings.>)
- [Google Sheets Knowledge Base](https://support.google.com/docs/thread/8978489/displaying-two-separate-formulas-in-one-cell-in-sheets?hl=en)
