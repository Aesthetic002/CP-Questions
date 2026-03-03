
## Problem Link [Here](https://leetcode.com/problems/minimum-flips-to-make-a-or-b-equal-to-c/description/)
## Tags  #Medium 
## Related Problems

## Topics [[Bit Manipulation]]

## Solutions

### Problem Statement

You are given three positive integers `a`, `b`, and `c`. The task is to find the minimum number of flips required in `a` or `b` to make the result of `(a OR b)` equal to `c`.

### Example

Input: `a = 2`, `b = 6`, `c = 5`

Binary Representation:

- `a = 2` is `010`
- `b = 6` is `110`
- `c = 5` is `101`

Output: `3` flips

### Approach 1: Bit-by-Bit Comparison

This approach involves iterating through the bits of `a`, `b`, and `c` simultaneously, from the least significant bit (LSB) to the most significant bit (MSB). For each bit position, we determine the necessary flips based on the current bits of `a`, `b`, and `c`.

#### Core Concepts

- **Extracting the Rightmost Bit:** To get the value of the rightmost bit (LSB) of any integer `N`, you can perform the bitwise AND operation: `N & 1`.
    - Example: `0101 & 1` results in `1`.
    - Example: `0100 & 1` results in `0`.
- **Right Shifting:** To effectively remove the current rightmost bit and move to the next bit for comparison, you can perform a right shift operation: `N >>= 1`.
    - Example: `0101` right-shifted by 1 (`>>= 1`) becomes `0010`.

#### Algorithm

1. Initialize a `flips` counter to `0`.
2. Use a `while` loop that continues as long as at least one of `a`, `b`, or `c` is greater than `0` (meaning there are still bits to process).
3. Inside the loop, for the current bit position:
    - Extract the rightmost bit of `a`: `bitA = a & 1`.
    - Extract the rightmost bit of `b`: `bitB = b & 1`.
    - Extract the rightmost bit of `c`: `bitC = c & 1`.
4. **Conditional Flip Logic:**
    - **If `bitC == 1` (Target bit is 1):**
        - We need `(bitA OR bitB)` to evaluate to `1`.
        - If `bitA` is `0` AND `bitB` is `0` (i.e., `0 OR 0 = 0`), then we need to flip at least one bit to `1`. Since we need a _minimum_ number of flips, we only need to flip one of them (e.g., `bitA` to `1` or `bitB` to `1`). Increment `flips` by `1`.
    - **If `bitC == 0` (Target bit is 0):**
        - We need `(bitA OR bitB)` to evaluate to `0`. This is only possible if both `bitA` and `bitB` are `0`.
        - If `bitA` is `1`, we must flip it to `0`. Increment `flips` by `1`.
        - If `bitB` is `1`, we must flip it to `0`. Increment `flips` by `1`.
        - _Note:_ If both `bitA` and `bitB` are `1`, both will be flipped, resulting in `flips` incrementing twice.
5. **Advance to Next Bit:** After processing the current rightmost bits, right shift `a`, `b`, and `c` by one position (`a >>= 1; b >>= 1; c >>= 1;`) to move to the next bit.
6. Once the loop finishes (all numbers become `0`), return the total `flips` count.

#### Example Walkthrough (Using `a=2 (010), b=6 (110), c=5 (101)`)

Initial: `flips = 0`

|a (binary)|b (binary)|c (binary)|bitA|bitB|bitC|(bitA OR bitB)|Target (bitC)|Flips (current)|Flips (total)|Reason|
|:--|:--|:--|:--|:--|:--|:--|:--|:--|:--|:--|
|010|110|101|||||||0||
|**Iteration 1 (LSB)** (1:54)|||||||||||
|010|110|101|0|0|1|0|1|+1|1|`bitC` is `1`, but `bitA` and `bitB` are `0`. Flip one of them.|
|After shift: 01|11|10|||||||||
|**Iteration 2** (3:03)|||||||||||
|01|11|10|1|1|0|1|0|+2|3|`bitC` is `0`, but `bitA` and `bitB` are `1`. Both must be flipped to `0`.|
|After shift: 0|1|1|||||||||
|**Iteration 3** (3:36)|||||||||||
|0|1|1|0|1|1|1|1|+0|3|`bitC` is `1`, and `(bitA OR bitB)` is `1`. No flips needed.|
|After shift: 0|0|0|||||||||
|Loop terminates as all are 0.|||||||||||

Final Answer: `3` flips.

#### Complexity Analysis

- **Time Complexity:** O(log(max(a, b, c))) or O(N), where N is the maximum number of bits required to represent the largest integer. For standard integers (e.g., 32-bit), this is effectively O(1).
- **Space Complexity:** O(1), as only a few variables are used.


---

### Approach 2: Using XOR and AND Operations

This approach is more concise and relies on the properties of bitwise operations, especially `XOR` and `AND`, combined with a built-in function to count set bits (`__builtin_popcount` in C++).

#### Algorithm

1. **Calculate the base mismatches:**
    
    - First, calculate `(a OR b)`. Let this be `val_ab`.
    - Then, compute the bitwise `XOR` of `val_ab` and `c`: `diff = val_ab ^ c`.
    - The `1`s in `diff` represent all the bit positions where `(a OR b)` did not match `c`. For each of these `1`s, at least one flip is required.
    - Initialize `flips = __builtin_popcount(diff)`. This function counts the number of set bits (1s) in `diff`.
2. **Account for "Double Flip" Scenarios:**
    
    - The initial `flips` count does not correctly handle a specific scenario: when the target bit `c` is `0`, but both `a` and `b` have `1` at that position.
    - Example: If `a_bit = 1`, `b_bit = 1`, and `c_bit = 0`.
        - `(a_bit OR b_bit)` is `1`.
        - `val_ab ^ c` will correctly show a `1` at this position, indicating a mismatch.
        - However, to change `(1 OR 1)` to `0`, you need to flip _both_ `a_bit` to `0` and `b_bit` to `0`, requiring `2` flips. `__builtin_popcount(diff)` only accounts for `1` flip here.
    - To find these "double flip" positions:
        - Identify positions where both `a` and `b` have a `1`: This is given by `(a & b)`.
        - From these, select only those positions where `c` was `0` (which implies a mismatch with `(a OR b)`). This can be found by `((a & b) & diff)`.
        - The `1`s in `((a & b) & diff)` represent the positions where an _extra_ flip is needed.
    - Add `__builtin_popcount((a & b) & diff)` to the `flips` total.
3. Return the total `flips`.
    

#### Example Walkthrough (Using `a=2 (010), b=6 (110), c=5 (101)`)

1. **`val_ab = a | b`**:
    - `a = 010`
    - `b = 110`
    - `val_ab = 110` (`010 OR 110 = 110`)
2. **`diff = val_ab ^ c`**:
    - `val_ab = 110`
    - `c = 101`
    - `diff = 011` (`110 XOR 101 = 011`)
3. **Initial `flips`**:
    - `__builtin_popcount(diff)` (`__builtin_popcount(011)`) = `2` (since there are two `1`s).
    - So, `flips = 2`.
4. **Calculate `(a & b)`**:
    - `a = 010`
    - `b = 110`
    - `a & b = 010` (`010 AND 110 = 010`)
5. **Calculate `extra_flips_mask = (a & b) & diff`**:
    - `a & b = 010`
    - `diff = 011`
    - `extra_flips_mask = 010` (`010 AND 011 = 010`)
    - This `010` indicates that at the second bit position (from right, 1-indexed), both `a` and `b` were `1`, and `val_ab` mismatched `c` (specifically, `val_ab` had `1` and `c` had `0`).
6. **Add `__builtin_popcount(extra_flips_mask)`**:
    - `__builtin_popcount(010)` = `1`.
    - `flips += 1`.
    - Total `flips = 2 + 1 = 3`.

Final Answer: `3` flips.

#### Complexity Analysis

- **Time Complexity:** O(1) in practice, as bitwise operations and `__builtin_popcount` operate on fixed-size integers (e.g., 32-bit or 64-bit) in constant time.
- **Space Complexity:** O(1).

## My Approach

- [ ] **Works**

```cpp

```


## Approach 1

- [x] **Works**

```cpp
// Approach 1: Bit-by-Bit Comparison
class Solution {
public:
    int minFlips(int a, int b, int c) {
        int flips = 0;

        while (a > 0 || b > 0 || c > 0) {
            int bitA = a & 1;  // Rightmost bit of a
            int bitB = b & 1;  // Rightmost bit of b
            int bitC = c & 1;  // Rightmost bit of c

            if (bitC == 1) {
                // If c wants 1 but both a and b have 0
                if (bitA == 0 && bitB == 0) {
                    flips++;
                }
            } else {
                // If c wants 0, both a and b must be 0
                if (bitA == 1) {
                    flips++;
                }
                if (bitB == 1) {
                    flips++;
                }
            }

            // Move to the next bit
            a >>= 1;
            b >>= 1;
            c >>= 1;
        }

        return flips;
    }
};
```


## Approach 2

- [x] **Works**

```cpp

class Solution {
public:
    int minFlips(int a, int b, int c) {
        // Bits where (a OR b) differs from c
        int diff = (a | b) ^ c;

        // At least one flip for each differing bit
        int flips = __builtin_popcount(diff);

        // Extra flips needed when a=1, b=1, c=0
        // (a & b) gives positions where both are 1
        // AND with diff ensures c is 0 at those positions
        flips += __builtin_popcount((a & b) & diff);

        return flips;
    }
};
```

