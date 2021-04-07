# 알고리즘 한 문제와 리뷰

***
## 리뷰
방의 크기를 구하는 알고리즘으로, 표준 입력을 통해 테스트 케이스가 주어지는만큼 수행한다. 
'+'는 벽, '.'은 빈방으로 표현한다.

vector<vector<int>> 변수로 설정한 방의 크기를 받아와
벽은 -1, 빈방은 0으로 초기화 한다.
 
DFS를 이용하여 방의 크기를 구한다.

map을 이용하여 방크기의 갯수를 구하여 출력한다.

***
### 입력예시
3 3

+++

+.+

+++

### 출력예시
1

1

***
## 코드
```
#include <iostream>
#include <vector>
#include <string>
#include <map>
#include <algorithm>
using namespace std;

void DFS(int , int , vector<vector<int> >&, int);

int main()
{
    int testCase;
    cin>>testCase;
    
    while(testCase--)
    {
        int row, col, roomNum=1;
        string line;
        cin>>col>>row;
        vector<vector<int> > maps(row, vector<int>(col, 0));
        
        
            cin.ignore();
        for(int i=0; i<row; i++)
        {
            getline(cin, line);
            for(int k=0; k<col; k++)
            {
                if(line[k]=='+')
                    maps[i][k]=-1;
            }
        }

        for(int i=0; i<row; i++)
            for(int k=0; k<col; k++)
            {
                if(maps[i][k]==0)
                {
                    DFS(i,k,maps,roomNum);
                    roomNum++;
                }
            }
               
     
    map<int, int, greater<int> > sum; 
    for(int i=0; i<row; i++)
        for(int k=0; k<col; k++)
        {
            if(maps[i][k]>0)
                sum[maps[i][k]]++;
        }
    

    for(auto e : sum){
        cout<<e.second<<" ";}

    cout<<endl;
    }
    
    return 0;
}

void DFS(int i, int j, vector<vector<int> >& maps, int roomNum)
{
    if(maps[i][j]==-1||maps[i][j]>0)
        return;

    maps[i][j] = roomNum;
    
    if(0<=i&&i<maps.size()-1)
        if(0<=j&&j<maps[i].size()-1)
        {
            DFS(i-1, j, maps, roomNum);
            DFS(i, j+1, maps, roomNum);
            DFS(i+1, j, maps, roomNum);
            DFS(i, j-1, maps, roomNum);
        }
}
```
