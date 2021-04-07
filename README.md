# 알고리즘 리뷰


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
        {
            for(int k=0; k<col; k++)
            {
                if(maps[i][k]==0){
                    DFS(i,k,maps,roomNum);
                    roomNum++;}
            }
        }
        
        

    map<int, int> sum; 
    for(int i=0; i<row; i++)
    {
        for(int k=0; k<col; k++)
        {
            if(maps[i][k]>0){
                sum[maps[i][k]]++;
            }
        }
    }

    vector <int> results;
    for(auto e : sum){results.push_back(e.second);} //graph hash function 
    sort(results.begin(), results.end());
    reverse(results.begin(), results.end());
    
    cout<<results.size()<<endl;

    for(int i=0; i<results.size(); i++)
        cout<<results[i]<<" ";

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
