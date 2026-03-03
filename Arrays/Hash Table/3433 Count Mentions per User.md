## Problem Link [Here](https://leetcode.com/problems/count-mentions-per-user/description/?envType=daily-question&envId=2025-12-12)
## Tags #Medium 
## Related Problems

## Topics [[Sets]] [[Simulation]]

## Solutions

### Approach: Playback After Sorting

#### Intuition

We first sort all events by time. For events with the same time, offline events should come first, because according to the problem statement, user state changes should be processed and synchronized before all other events that occur at the same time.

After sorting, we process each event in chronological order from front to back. We can use a hash table to record each user's online time, and determine whether the user is online by comparing it with the current time. During traversal:

1. For message events, the cases where the mentioned object is ALL or HERE are relatively easy to handle. However, for the other case, we need to parse a \textit{mentions_string} that contains multiple specified ids. This string is composed of multiple idx separated by spaces, where x is the integer we need to parse. In most languages, we can concatenate consecutive digits to form an id and split when we reach the end of the string or the next character is a space. For languages that provide a string split method, we can split the string by space split, then remove the prefix of each entry to obtain each user id.
2. For offline events, set the user's online status in the hash table for sixty units of time after the event.

#### Complexity Analysis

Let n be numberOfUsers, m be the length of events, and t be the maximum timestamp.

- Time complexity: O(nm+mlogmlogt).
    
    The time complexity of sorting events is O(mlogmlogt), and timestamp parsing takes O(logt). Traversing and processing each event takes O(nm).
    
- Space complexity: O(n).


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    vector<int> countMentions(int n, vector<vector<string>>& e) {

        // Sort by timestamp; if equal timestamp, OFFLINE comes before MESSAGE
        sort(e.begin(), e.end(), [](const auto& a, const auto& b) {
            int ta = stoi(a[1]);
            int tb = stoi(b[1]);

            if (ta != tb)
                return ta < tb;   // sort by timestamp

            // timestamps equal -> OFFLINE before MESSAGE
            if (a[0] != b[0])
                return a[0] == "OFFLINE";

            return false; // keep original order
        });

        vector<int> mp(n);
        unordered_set<int> online;

        // initialize all users online
        for (int i = 0; i < n; i++)
            online.insert(i);

        set<pair<int, int>> offline;   // {userId, offlineStartTime}

        for (auto i : e) {

            // Check if any offline users should auto-return online
            if (!offline.empty()) {
                vector<pair<int, int>> toErase;

                for (auto j : offline) {
                    if (stoi(i[1]) - 60 >= j.second) {
                        online.insert(j.first);
                        toErase.push_back(j);
                    }
                }

                for (auto& p : toErase)
                    offline.erase(p);
            }

            // Process MESSAGE
            if (i[0] == "MESSAGE") {

                if (i[2] == "HERE") {
                    for (auto z : online)
                        mp[z]++;
                } 
                else if (i[2] == "ALL") {
                    for (auto& z : mp)
                        z++;
                } 
                else {
                    // Parse "id<number> id<number>" manually
                    string yo = "";

                    for (int z = 0; z < i[2].size(); z++) {
                        char ch = i[2][z];

                        if (ch == ' ') {
                            mp[stoi(yo)]++;
                            yo.clear();
                            continue;
                        }
                        else if (ch != 'i' && ch != 'd') {
                            yo.push_back(ch);
                        }

                        // Last token
                        if (z == i[2].size() - 1) {
                            mp[stoi(yo)]++;
                            yo.clear();
                            break;
                        }
                    }
                }
            } 

            // Process OFFLINE
            else {
                online.erase(stoi(i[2]));
                offline.insert({stoi(i[2]), stoi(i[1])});
            }
        }

        return mp;
    }
};

```


## Editorial Approach

- [ ] **Works**

```cpp
class Solution {
public:
    vector<int> countMentions(int numberOfUsers,
                              vector<vector<string>>& events) {
        vector<int> count(numberOfUsers);
        vector<int> next_online_time(numberOfUsers);
        sort(events.begin(), events.end(),
             [&](const vector<string>& lth, const vector<string>& rth) {
                 int lth_timestamp = stoi(lth[1]);
                 int rth_timestamp = stoi(rth[1]);
                 if (lth_timestamp != rth_timestamp) {
                     return lth_timestamp < rth_timestamp;
                 }
                 if (rth[0] == "OFFLINE") {
                     return false;
                 }
                 return true;
             });

        for (auto&& event : events) {
            int cur_time = stoi(event[1]);
            if (event[0] == "MESSAGE") {
                if (event[2] == "ALL") {
                    for (int i = 0; i < numberOfUsers; i++) {
                        count[i]++;
                    }
                } else if (event[2] == "HERE") {
                    for (int i = 0; i < numberOfUsers; i++) {
                        if (next_online_time[i] <= cur_time) {
                            count[i]++;
                        }
                    }
                } else {
                    int idx = 0;
                    for (int i = 0; i < event[2].size(); i++) {
                        if (isdigit(event[2][i])) {
                            idx = idx * 10 + (event[2][i] - '0');
                        }
                        if (i + 1 == event[2].size() ||
                            event[2][i + 1] == ' ') {
                            count[idx]++;
                            idx = 0;
                        }
                    }
                }
            } else {
                int idx = stoi(event[2]);
                next_online_time[idx] = cur_time + 60;
            }
        }
        return count;
    }
};
```


## Approach 2

- [ ] **Works**

```cpp

```