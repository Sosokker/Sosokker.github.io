---

---
[Problem](https://theory.cpe.ku.ac.th/wiki/index.php/Algo_lab/zooma_1) [Code Template](https://theory.cpe.ku.ac.th/~jittat/algo-lab/zooma/)

---
## Explain

![250](https://cdn.cloudflare.steamstatic.com/steam/apps/3330/0000000522.1920x1080.jpg?t=1627918693)
#### Component

1. **N** *sequence of colored balls* move toward to an exit  
2. **M** *colored balls to shoot* into the sequence

#### Goal

**Final sequence of the balls** After we shoot all *M* ball into sequence of *N* ball

#### Input
<p>Color of ball indicate by: <span style="color: green;">G = 1</span>, <span style="color: blue;">B = 2</span>, <span style="color: yellow;">Y = 3</span>, <span style="color: red;">R = 4</span>.</p>

- Two integers **n** and **m**
	- **n** -> the length of the original sequence.
	- **m** -> the number of additional balls to shoot(insert).
- **n** lines to tell about color of ball
- **m** lines, each containing two integers:
	- **d** -> the color of the additional ball (Ball to shoot).
	- **p** -> Insert Ball color **d** to *after ball **#p+1** in sequence n* .

##### Example
**Input**
5 4  -> 5 =(`n`) of the original sequence of balls , 4 = the number (`m`) balls that you can shoot
1 -> <span style="color: green;">Green Ball at position #1</span> 
Ball sequence : ==1==
2 -> <span style="color: Blue;">Blue Ball at position #2</span> 
Ball sequence : 1 ==2==
1 -> <span style="color: green;">Green Ball at position #3</span>
Ball sequence : 1 2 ==3==
3 -> <span style="color: Yellow;">Yellow Ball at position #4</span>
Ball sequence : 1 2 3 ==4==
3 -> <span style="color: Yellow;">Yellow Ball at position #5</span>
Ball sequence : 1 2 3 4 ==5==
4 3 -> Insert <span style="color: Red;">Red ball</span> after the <span style="color: green;">ball Number 3</span> in sequence, **Now this ball is #6**
Ball sequence : 1 2 3 ==6== 4 5
1 1 -> Insert <span style="color: Green;">Green ball</span> after the <span style="color: green;">ball Number 1</span> in sequence, **Now this ball is #7** 
Ball sequence : 1 ==7== 2 3 6 4 5
2 6 -> Insert <span style="color: Blue;">Blue ball</span> after the <span style="color: Red;">ball #6</span> in sequence, **Now this ball is #8**
Ball sequence : 1 7 2 3 6 ==8== 4 5
1 5 -> Insert <span style="color: Green;">Green ball</span> after the <span style="color: Yellow;">ball #5</span> in sequence, **Now this ball is #9**
Ball sequence : 1 7 2 3 6 4 5 ==9==

**Output**
1
7
2
3
6
8
4
5
9

## Idea and Concept

#### What we have
1. Original Ball Sequence
2. Ball to insert or shoot

#### Key Operation
1. Insert new ball to sequence
2. Shifting Existing Ball after Insert
3. Keep track the sequence

Sequence + Insert + Shift + Track the Sequence
1. **Array** or **Vector** 
2. **Queue** 

## How to Solve

#### Initialization

1. something to store colors of the balls in sequence = **array**
2. something to represent current sequence of ball
3. something that can insert ball to the sequence
	1. Insert at the end of sequence (To add new **N** ball)
	2. Insert at any location, shift the rest of the ball (To insert new **M** ball)
---
## Solution

```cpp
#include <iostream>
using namespace std;

const int MAX_N = 2000100;

int c[MAX_N];
int balls[MAX_N];
int ball_count = 0;

void insert_end(int lst[], int& s, int val)
{
    lst[s] = val;
    s++;
}

int find(int lst[], int s, int target)
{
    for (int i = 0; i < s; i++) {
    if (lst[i] == target) {
        return i;
    }
    }
    return -1;

}

int insert(int lst[], int& s, int val, int loc)
{
    for (int i = s; i > loc; i--) {
    lst[i] = lst[i - 1];
    }
    lst[loc] = val;
    s++;
    return s;
}

int main()
{
    int n, m;
    int d, p;
  
    cin >> n >> m;
    for (int i = 0; i < n; i++) {
        cin >> c[i];
        insert_end(balls, ball_count, i + 1);
    }

    for (int i = 0; i < m; i++) {
        cin >> d >> p;
        int idx = find(balls, ball_count, p);
        insert(balls, ball_count, i + n + 1, idx + 1);
    }

    for (int i = 0; i < ball_count; i++) {
        cout << balls[i] << endl;
    }
  return 0;
}
```