## Converting HEX Color to RGB in JavaScript

### 1. Recognizing HEX Components
A HEX color format consists of 6 characters (excluding the '#').
- The first two characters represent the **red (R)** color.
- The next two represent the **green (G)** color.
- The last two represent the **blue (B)** color.

### 2. Converting HEX Components to Decimal Values
To convert a HEX value to a decimal value, you can use the `parseInt` function in JavaScript.

Example:
```javascript
let decimalValue = parseInt("9A", 16);
```

### 3. Retrieving RGB Values
After converting all three HEX components to decimal values, you will have three decimal values corresponding to the R, G, and B colors.

**Steps for conversion**:
1. Remove the '#' character from the HEX string.
2. Take the first two characters (for R) and convert them to a decimal value.
3. Take the next two characters (for G) and convert them to a decimal value.
4. Take the last two characters (for B) and convert them to a decimal value.
