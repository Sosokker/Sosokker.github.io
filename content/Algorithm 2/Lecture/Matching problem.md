## What is matching problem

Let's say we have D and R (Domain and Range)
where $M \subset D,R$ | $M = pair(a,b)$

then $\forall a\in D$ must exist once in $M$
and $\forall b\in R$ must exist once in $M$
## Stable Marriage Matching Problem

- M -> set of n man
- W -> set of n woman

Given M and W, find a **stable matching** of size n

#### What is **Stable Matching**?
Let define *unstable pair*
- A pair $(m,w)$ is *unstable* if and only if
	-  $m$ prefer other girl to $w$ : m prefer other girl $w^{\prime}$ to $w$  
	-  that girl $(w^{\prime})$ other than $w$ also prefer m to her partner

In the other word, matching is *stable* when there *does not exist* any pair $(m, w)$ which both prefer each other *to their current partner*.

we will revised the stable matching problem a little bit where each men and women have their own *preference* : we will call it **Different Stable Matching**

##### Different Stable Matching

Suppose there are four men and women

Men : A, B, C, D , Women: a, b, c, d

$A[a>b>c>d]$ ------ $a[A>C>B>D]$
$B[a>c>b>d]$ ------ $b[B>D>A>C]$
$C[b>d>c>a]$ ------ $c[C>D>B>A]$
$D[b>a>d>c]$ ------ $d[B>A>D>C]$

Are there any algorithm to find all solution for stable pair?

## Gale-Shapley algorithm
or deferred acceptance algorithm / propose and reject algorithm can use to solve those problem!

#### Pseudocode
```python
start with free m and w
while (still have free m):
	m propose to some w where not yet been proposed by m
	if there exist some pair of (m_old, w):
	   if w prefer m to m_old:
	      engange m -> (m, w)
	      free m_old
		else:
			reject m
	else:
		engange (m,w)
```

#### Python
```python
def gale_shapley(men_prefs, women_prefs):
    n = len(men_prefs)
    women_partner = [-1] * n
    men_engaged = [False] * n
    free_men = n

    while free_men > 0:
        m = next((i for i, engaged in enumerate(men_engaged) if not engaged), None)

        for w in men_prefs[m]:
            if women_partner[w] == -1:
                women_partner[w] = m
                men_engaged[m] = True
                free_men -= 1
            else:
                m1 = women_partner[w]
                if women_prefs[w].index(m) < women_prefs[w].index(m1):
                    women_partner[w] = m
                    men_engaged[m] = True
                    men_engaged[m1] = False

    # Print the stable matches
    print("Stable Matches:")
    for i, m in enumerate(women_partner):
        print(f"Woman {i} is matched to Man {m}")

# Example preferences (lower index indicates higher preference)
men_prefs = [[1, 0], [1, 0]]
women_prefs = [[0, 1], [0, 1]]

gale_shapley(men_prefs, women_prefs)
```
#### C++
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// Function to perform Gale-Shapley algorithm
void galeShapley(vector<vector<int>>& menPrefs, vector<vector<int>>& womenPrefs) {
    int n = menPrefs.size();
    vector<int> womenPartner(n, -1);
    vector<bool> menEngaged(n, false);
    int freeMen = n;

    while (freeMen > 0) {
        int m;
        for (m = 0; m < n; ++m) {
            if (!menEngaged[m]) {
                break;
            }
        }

        for (int i = 0; i < n && !menEngaged[m]; ++i) {
            int w = menPrefs[m][i];
            if (womenPartner[w] == -1) {
                womenPartner[w] = m;
                menEngaged[m] = true;
                freeMen--;
            } else {
                int m1 = womenPartner[w];
                if (find(womenPrefs[w].begin(), womenPrefs[w].end(), m) <
                    find(womenPrefs[w].begin(), womenPrefs[w].end(), m1)) {
                    womenPartner[w] = m;
                    menEngaged[m] = true;
                    menEngaged[m1] = false;
                }
            }
        }
    }

    // Print the stable matches
    cout << "Stable Matches:" << endl;
    for (int i = 0; i < n; ++i) {
        cout << "Woman " << i << " is matched to Man " << womenPartner[i] << endl;
    }
}

int main() {
    // Example preferences (lower index indicates higher preference)
    vector<vector<int>> menPrefs = {{1, 0}, {1, 0}};
    vector<vector<int>> womenPrefs = {{0, 1}, {0, 1}};

    galeShapley(menPrefs, womenPrefs);

    return 0;
}

```
