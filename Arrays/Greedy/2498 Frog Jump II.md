## Problem Link [Here](https://leetcode.com/problems/frog-jump-ii/description/)

### Related Problems

### Topics [[Binary Search]] [[Greedy]]

### [Solutions]()


## My Approach

```cpp
class Solution {

public:

    int maxJump(vector<int>& stones) {

        int a=0,n=stones.size();

        for(int i=0;i<n-1;i+=2){

            if(i==n-2){

            a=max(a,abs(stones[i]-stones[i+1]));

            }

            else{

            a=max(a,abs(stones[i]-stones[i+2]));

            }

            if(i)

            stones[i]=-1;

        }

    int p=stones[n-1];

        for(int i=n-2;i>=0;i--){

            if(stones[i]!=-1){

                a=max(a,abs(p-stones[i]));

                p=stones[i];

            }

        }

  

        return a;

    }

};
```


## Approach 1

```cpp

class Solution
{
    public:
    LOGIC

    KARNA KYA HAIN❓
    1. Stones are given in strictly increasing order representing positions
    of stones in a river.
    2. Frog is initially oin a 1st stone and usko last stone pe jana hain and
    then return to the 1st stone.
    3. It can jump to any stone at most once.(Matlab forward path traverse karte
    jo stone pe kude the unpe wapas aate samay dobara nahin kud sakte.)
    4. Length of jump = |stones[i] - stones[j]|.
    5. Cost of path = Max len of jump among all jumps in path
    6. Return the min cost of a path for the frog.

    APPROACH & INTUITION
    1. Minimum Cost and Increasing Order dekhke - Greedy Strike karega💡.
    2. BS on answers can also be an approach. Why❓
    - Strictly increasing order.
    - Cost of path will be in range [0,maxPos-minPos]

    3. GREEDY SOL APPROACH
    - Agar kisi path pe hame forward jaana hain aur vapis aana hain provided that
    wapas aane jaane mein ham stone pe ek hi baar kude.
    - Then its logical ki in forward and backward we jump on alternate stones.
    - So while moving in forward direction we will jump on alternate stones
    i and i+2. Inka max diff nikalenge joki cost hogi hamari.
    - Yeh min Cost kaise hogi❓-> We are making sure to find max of alternate 
    stones and the gap of 2-3 stones is not there so we are finding the most 
    optimal path and cost jisse back and forward dono mein traverse karle.
    - Backward direction and forward direction dono mein jaane mein ya to cost
    same ya kam lage.

    4. BINARY SEARCH
    - Reasons are state above for using BS on answers.
    - low=0,high = stones[n-1]-stones[0]
    - We will find mid cost and check if backward and forward direction both
    possible or not .
    - If possible then mid=high (Trying to find more optimal min cost)
    - If not possible then we will increase the cost for traversing in both 
    direction.
    - While checking for forward direction jo stones ham cover kar rahe hain
    unki visited mark kardenge.
    - Jisse Backward test ke time pe un stones pe jump na kare.
//========================================================================================================

       	//GREEDY SOL (LOGIC EXPLAINED ABOVE)
       	int maxJump(vector<int>& stones) {
       	     int n = stones.size();
       	     int maxi = INT_MIN;
       	     if(n==2)
       	     return stones[n-1]-stones[0];
       	     for(int i=0;i < n-2;i++)
       	     {
                 //Finding diff between alternate stone pos
                 //The max cost found is the min cost of the path
       	         maxi = max(maxi,stones[i+2]-stones[i]);
       	     }
       	     return maxi;
       	 }

       	//BS ON ANSWERS
        bool isPossible(int cost, vector<int> &stones)
        {
            int n = stones.size();
            vector<bool> visited(n, false);
            //Array to mark the stones pos which are visited
            //so that they are not traversed in backward direction
            int ind = 0;
            while (ind < n - 1)
            //Checking in forward direction
            {
                int j = ind;
                //j se lekar i tak jitni pos cover ho rahi unko cover karlo
                //Goal is to minimize the number of stones jumped.
                while (j + 1 < n && stones[j + 1] <= stones[ind] + cost)
                    j++;
                if (j == ind)
                //Agar j badha hi nahin vahin ka vahin rahe gaya
                    return false;
                ind = j;
                //Updated position to the stone jumped
                visited[ind] = true;
                //Making the stone visited
            }

            //Optional we could have check while traversing
            //Storing positions of stones which are still to bs visited
            //Completely removing the visited Stone positions
            vector<int> indexes;
            for (int j = 0; j < n - 1; j++)
            {
                if (visited[j] == false) indexes.push_back(j);
            }
            indexes.push_back(n - 1);

            //Checking for backward direction
            ind = indexes.size() - 1;
            while (ind > 0)
            {
                int j = ind;
                //Covering as much stones as possible
                while (j > 0 && stones[indexes[j - 1]] >= stones[indexes[j]] - cost)
                    j--;
                if (j == ind)
                    return false;
                ind = j;
                //Updating the stone position
            }
            return true;
        }
    int maxJump(vector<int> &stones)
    {
        int n = stones.size();
        int low = 0;
        int high = stones[n - 1] - stones[0];
        //Range of cost
        while (low <= high)
        {
            int mid = (low + high) / 2;
            if (isPossible(mid, stones))
            //Whether it is possible to traverse in both directions 
            {
                high = mid - 1;
                //If possible then we will try to find more optimal lower cost
            }
            else
                low = mid + 1;
                //The cost required is higher then expected
        }
        return low;
    }
};

```


## Approach 2

```cpp

```