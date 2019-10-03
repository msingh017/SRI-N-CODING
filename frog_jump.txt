#include<iostream>
using namespace std;
int a[100][100];
int visit[100][100];

int x_move[]={-1,0,1,0};
int y_move[]={0,1,0,-1};

bool check(int x,int y,int n,int m){
	if(x<0 || y<0 || x>=n || y>=m || a[x][y]==0 || visit[x][y]==1)return false;
	return true;
}

void find_dis(int sx,int sy,int dx,int dy,int n,int m,int count,int &min_count){
	if(sx==dx && sy==dy){
		//cout<<count<<endl;
		if(count<min_count)min_count=count;
		return;
	}
	for(int i=0;i<4;i++){
		int new_x=sx+x_move[i];
		int new_y=sy+y_move[i];
		if(check(new_x,new_y,n,m)){
			visit[new_x][new_y]=1;
			if(i==1 || i==3)find_dis(new_x,new_y,dx,dy,n,m,count,min_count);
			else find_dis(new_x,new_y,dx,dy,n,m,count+1,min_count);
			visit[new_x][new_y]=0;
		}
	}
}

int main(){
	int test;
	cin>>test;
	while(test--){
		int n,m;
		cin>>n>>m;
		for(int i=0;i<n;i++)for(int j=0;j<m;j++)cin>>a[i][j];
		int sx,sy,dx,dy;
		cin>>sx>>sy>>dx>>dy;
		if(a[sx][sy]==0 || a[dx][dy]==0)cout<<"-1"<<endl;
		else if(sx==dx && sy==dy)cout<<"0"<<endl;
		else{
			for(int i=0;i<n;i++)for(int j=0;j<m;j++)visit[i][j]=0;
			int min_count=1000001;
			visit[sx][sy]=1;
			find_dis(sx,sy,dx,dy,n,m,0,min_count);
			if(min_count==1000001)min_count=-1;
			cout<<min_count<<endl;
		}
	}
	return 0;
}