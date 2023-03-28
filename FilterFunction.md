Yes, you can create a custom code function in your report to handle this more efficiently. This will make the expression in your report shorter and easier to understand.

To create a custom code function, follow these steps:

1. In the Report Designer, open the Report Properties dialog.
2. Go to the "Code" tab.
3. Add the following custom code function:



```vb
Function FormatDoubleWithoutRounding(value As Double, decimals As Integer) As String
    Dim stringValue As String = value.ToString("F99").TrimEnd("0"c).TrimEnd("."c)
    Dim decimalIndex As Integer = stringValue.IndexOf("."c)

    If decimalIndex = -1 Then
        Return stringValue & "." & New String("0"c, decimals)
    Else
        Dim decimalPartLength As Integer = stringValue.Length - decimalIndex - 1
        If decimalPartLength < decimals Then
            Return stringValue & New String("0"c, decimals - decimalPartLength)
        Else
            Return stringValue.Substring(0, decimalIndex + decimals + 1)
        End If
    End If
End Function
```

This custom function will take a double value and the desired number of decimal places as input, and it will return the formatted string without rounding.

4. Now, you can use this custom function in your report's expression like this:

```vb
=Code.FormatDoubleWithoutRounding(Fields!YourValue.Value, 7)
```

Replace Fields!YourValue.Value with the field or expression representing your double value. This should give you the desired output more efficiently while keeping the expression short and easy to understand.
