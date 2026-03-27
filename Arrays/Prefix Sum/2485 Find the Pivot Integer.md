## Problem Link [Here](https://leetcode.com/problems/find-the-pivot-integer/description/)
## Tags #Easy 
## Related Problems

## Topics [[Prefix Sum]]  [[Binary Search]]  [[Math]]  [[Two Pointers]]

## Solutions


## My Approach (Prefix)

- [x] **Works**

```cpp
class Solution {
public:
    int pivotInteger(int n) {
        vector<int>pref(n),suf(n);
        pref[0]=0;
        for(int i=1;i<n;i++){
            pref[i]=pref[i-1]+i;
        }
        suf[n-1]=0;
        for(int i=n;i>1;i--){
            suf[i-2]=suf[i-1]+i;
        }

        for(int i=1;i<=n;i++){
            if(suf[i-1]==pref[i-1])return i;
        }
        return -1;
    }
};
```


## Brute Force

- [x] **Works**

```cpp
class Solution {
public:
    int pivotInteger(int n) {
        // Iterate through possible pivot values
        for (int i = 1; i <= n; i++) {
            int sumLeft = 0;
            int sumRight = 0;

            // Calculate the sum of elements on the left side of the pivot
            for (int j = 1; j <= i; j++) {
                sumLeft += j;
            }

            // Calculate the sum of elements on the right side of the pivot
            for (int k = i; k <= n; k++) {
                sumRight += k;
            }

            // Check if the sums on both sides are equal
            if (sumLeft == sumRight) {
                return i; // Return the pivot value if found
            }
        }

        return -1; // Return -1 if no pivot is found
    }
};
```


## Binary Search

- [x] **Works**

```cpp
class Solution {
public:
    int pivotInteger(int n) {
        // Initialize left and right pointers for binary search
        int left = 1, right = n;
        
        // Calculate the total sum of the sequence
        int totalSum = n * (n + 1) / 2;

        // Binary search for the pivot point
        while (left < right) {
            // Calculate the mid-point
            int mid = (left + right) / 2;

            // Check if the difference between the square of mid and the total sum is negative
            if (mid * mid - totalSum < 0) {
                left = mid + 1; // Adjust the left bound if the sum is smaller
            } else {
                right = mid; // Adjust the right bound if the sum is equal or greater
            }
        }

        // Check if the square of the left pointer minus the total sum is zero
        if (left * left - totalSum == 0) {
            return left;
        } else {
            return -1;
        }
    }
};
```

## Two Pointers

- [x] **Works**

```cpp
class Solution {
public:
    int pivotInteger(int n) {
        int leftValue = 1;
        int rightValue = n;
        int sumLeft = leftValue;
        int sumRight = rightValue;

        if (n == 1) return n;
        
        // Iterate until the pointers meet
        while (leftValue < rightValue) {
            // Adjust sums and pointers based on comparison
            if (sumLeft < sumRight) {
                sumLeft += ++leftValue;
            } else {
                sumRight += --rightValue;
            }

            // Check for pivot condition
            if (sumLeft == sumRight && leftValue + 1 == rightValue - 1) {
                return leftValue + 1;
            }
        }

        return -1; // Return -1 if no pivot is found
    }
};
```

## Math

- [x] **Works**

```cpp
class Solution {
 public:
  int pivotInteger(int n) {
        const int sum = (n * (n + 1) / 2);
        const int pivot = sqrt(sum);
        // If pivot * pivot is equal to sum (pivot found) return pivot, else return -1
        return pivot * pivot == sum ? pivot : -1;
  }
};
```

## Approach 2

- [ ] **Works**

```cpp

```