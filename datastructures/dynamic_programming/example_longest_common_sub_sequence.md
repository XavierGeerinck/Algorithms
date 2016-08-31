# Example : Longest Common Sub sequence
The longest common subsequence algorithm, is a Dynamic Programming algorithm that will find the longest appearing subsequence in 2 strings of text.

Finding this with Dynamic Programming is really easy. We will create a matrix for the 2 strings and fill in the matrix from the top to bottom, left to right. 

1. Create a matrix for the 2 strings
2. Insert a 0 row and a 0 column
3. Go from top to bottom left to right
    * Check the 2 characters of the 2 strings and the current index
        * If they match, do the previous value + 1
        * Else, take the maximum of the value above and the value at the left
4. Continue this for every field in the matrix

To now find our LGC, we start that the most right bottom value in our matrix, and go back. If the characters match, we go one diagonally left upwards, else we go left.

## Example
![](/images/datastructures/dynamic_programming_longest_common_subsequence.png)

## Code

```
/**
 * @author: Xavier Geerinck
 * @title: Longest Common Subsequence
 * @subtitle: This algorithm finds the longest common subsequence in 2 different strings
 * @method:
 * To find the longest common subsequence, we will create a matrix with at the top the first string and at the left the second string. 
 * 1. Set length of the LCS = 0
 * 2. From left to right, top to bottom, loop over the matrix
 *     i. If the characters are equal at i, j --> do LCS + 1
 *     ii. If the characters are not equal at i,j --> take max(leftVal, topVal)
 */
var stringA = "aloysius";
var stringB = "louis";

var stringA = "ABCDGH";
var stringB = "AEDFHR";

var matrix = [];

for (var i = 0; i < stringB.length; i++) {
    for (var j = 0; j < stringA.length; j++) {
    		if (!matrix[i]) {
            matrix[i] = [];
        }
        
        if (stringA.charAt(j) == stringB.charAt(i)) {
            matrix[i][j] = (j - 1) >= 0 ? matrix[i][j - 1] + 1 : 1;
        } else {
            var left = (j - 1) >= 0 ? matrix[i][j - 1] : 0;
            var top = (i - 1) >= 0 ? matrix[i - 1][j] : 0;
            
            matrix[i][j] = Math.max(left, top);
        }
    }
}

var str = "The longest Common Subsequence = " + matrix[stringB.length - 1][stringA.length - 1] + "<br /><br />";
str += "This is the string: ";

var sol = "";
for (var i = stringB.length - 1; i >= 0; i--) {
    for (var j = stringA.length - 1; j >= 0; j--) {
        if (stringA.charAt(j) == stringB.charAt(i)) {
            sol += stringA.charAt(j) + " ";
            i--;
        }
    }
}

str += Array.from(sol).reverse().join('');

str += "<br /><br />With the following matrix: <br />"

for (var i = 0; i < stringB.length; i++) {
    for (var j = 0; j < stringA.length; j++) {
        str += matrix[i][j] + " ";
    }
    
    str += "<br />";
}

document.querySelector("#result").innerHTML = str;
```
