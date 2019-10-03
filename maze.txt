#include<iostream>
using namespace std;
int a[11][11];
int visit[11][11];
int x_move[]={-1,0,1,0};
int y_move[]={0,1,0,-1};

bool check(int x,int y,int n){
	if(x<1 || x>n || y<1 || y>n || visit[x][y]==1 || a[x][y]==1)return false;
	return true;
}

void calculate(int sx,int sy,int dx,int dy,int n,int count,int &max_jewels){
	if(sx==dx && sy==dy){
		if(count>max_jewels)max_jewels=count;
		return;
	}
	for(int i=0;i<4;i++){
		int new_sx=sx+x_move[i];
		int new_sy=sy+y_move[i];
		if(check(new_sx,new_sy,n)){
			visit[new_sx][new_sy]=1;
			if(a[new_sx][new_sy]==2)calculate(new_sx,new_sy,dx,dy,n,count+1,max_jewels);
			else calculate(new_sx,new_sy,dx,dy,n,count,max_jewels);
			visit[new_sx][new_sy]=0;
		}
	}
}

int main(){
	ios_base::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	int test;
	cin>>test;
	while(test--){
		int n;
		cin>>n;
		for(int i=1;i<=n;i++)for(int j=1;j<=n;j++)cin>>a[i][j];
		int sx,sy,dx,dy;	           //source and destination location
		cin>>sx>>sy>>dx>>dy;
		for(int i=1;i<=n;i++)for(int j=1;j<=n;j++)visit[i][j]=0;
		int max_jewels=0;
		int count=0;
		if(a[sx][sy]==2)count=1;
		visit[sx][sy]=1;
		calculate(sx,sy,dx,dy,n,count,max_jewels);
		cout<<max_jewels<<endl;
	}
	return 0;
}