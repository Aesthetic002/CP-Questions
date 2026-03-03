## Problem Link [Here]()

## Related Problems

## Topics

## Solutions


## My Approach

- [ ] **Works**

```cpp
class Solution {

public:

    double slope(vector<int>& y, vector<int>& z) {

        if (y[0] == z[0])

            return 10000;

  

        return (double)(z[1] - y[1]) / (double)(z[0] - y[0]);

    }

    int countTrapezoids(vector<vector<int>>& p) {

        int n = p.size();

        map<pair<vector<int>, vector<int>>, double> yo;

        map<double, vector<pair<vector<int>, vector<int>>>> mp;

        for (int i = 0; i < n - 1; i++) {

            for (int j = i + 1; j < n; j++) {

                yo[{p[j], p[i]}] = slope(p[j], p[i]);

                mp[yo[{p[j], p[i]}]].push_back({p[j], p[i]});

            }

        }

        long long ans = 0;

        for (auto i : mp) {

            for (int j = 0; j < i.second.size() - 1; j++) {

                for (int k = j + 1; k < i.second.size(); k++) {

                    if ((i.second[k].first != i.second[j].first) &&

                        (i.second[k].first != i.second[j].second) &&

                        (i.second[k].second != i.second[j].first) &&

                        (i.second[k].second != i.second[j].second)) {

                        if ((yo[{i.second[k].first, i.second[j].second}] !=

                             yo[{i.second[k].second, i.second[j].first}]) ||

                            ((yo[{i.second[k].first, i.second[j].first}] !=

                              yo[{i.second[k].second, i.second[j].second}]))) {

                            ans++;

                        }

                    }

                }

            }

        }

        return ans;

    }

};
```


## Approach 1

- [x] **Works**

```cpp
class Solution {
public:
    using ll = long long;

    int countTrapezoids(vector<vector<int>>& p) {
        int n = p.size();

        // slope → list of segments (i, j)
        unordered_map<ll, vector<pair<int,int>>> buckets;

        auto gcdll = [&](int a, int b) {
            return std::gcd(a, b);
        };

        auto encodeSlope = [&](int dx, int dy) {
            // normalize to unique direction
            if (dx < 0) dx = -dx, dy = -dy;
            if (dx == 0 && dy < 0) dy = -dy;
            return ( (ll)dx << 32 ) | (unsigned int)dy;
        };

        // ───────────────────────────────────────────────
        // STEP 1: build slope buckets
        // ───────────────────────────────────────────────
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int dx = p[j][0] - p[i][0];
                int dy = p[j][1] - p[i][1];
                int g = gcdll(abs(dx), abs(dy));
                dx /= g; dy /= g;
                ll key = encodeSlope(dx, dy);
                buckets[key].push_back({i, j});
            }
        }

        long long totalTrapezoidPairs = 0;
        long long parallelogramCount = 0;

        // ───────────────────────────────────────────────
        // STEP 2: For each slope bucket of size k,
        //         total base-pairs = C(k,2)
        //         then subtract pairs sharing endpoints
        // ───────────────────────────────────────────────
        for (auto &entry : buckets) {
            auto &seg = entry.second;
            int k = seg.size();
            if (k < 2) continue;

            long long totalPairs = 1LL * k * (k - 1) / 2;

            // subtract pairs sharing endpoints
            unordered_map<int,int> freq;
            for (auto &s : seg) {
                freq[s.first]++;
                freq[s.second]++;
            }
            for (auto &f : freq) {
                int c = f.second;
                if (c >= 2) totalPairs -= 1LL * c * (c - 1) / 2;
            }

            totalTrapezoidPairs += totalPairs;

            // ───────────────────────────────────────────
            // STEP 3: parallelogram detection via midpoint hashing
            // ───────────────────────────────────────────
            unordered_map<ll,int> midCount;

            for (auto &s : seg) {
                int a = s.first, b = s.second;

                ll mx = (ll)p[a][0] + p[b][0];
                ll my = (ll)p[a][1] + p[b][1];

                ll key = (mx << 32) ^ (unsigned long long)my;
                midCount[key]++;
            }

            for (auto &mc : midCount) {
                int c = mc.second;
                if (c >= 2) parallelogramCount += 1LL * c * (c - 1) / 2;
            }
        }

        // ───────────────────────────────────────────────
        // STEP 4: Every parallelogram was counted twice.
        // Subtract once to make count correct.
        // ───────────────────────────────────────────────
        return totalTrapezoidPairs - parallelogramCount;
    }
};

```


## Approach 2

- [ ] **Works**

```cpp

```