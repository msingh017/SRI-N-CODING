#include<iostream>
using namespace std;
int matrix[1000][1000];
int dis[1000][1000];
int x_move[]={-1,0,1,0};
int y_move[]={0,1,0,-1};

struct queue1{
	int x;
	int y;
};

queue1 q[100000];
queue1 pair1;
int start1,end1;

bool check(int nx,int ny,int n,int m){
	if(nx<1 || nx>n || ny<1 || ny>m || dis[nx][ny]!=-1 || matrix[nx][ny]==0)return false;
	return true;
}

void calculate_bfs(int dx,int dy,int n,int m){
	while(start1!=end1){
		int ax=q[start1].x;
		int ay=q[start1].y;
		start1++;
		dis[ax][ay]=0;
		for(int i=0;i<4;i++){
			int new_x=ax+x_move[i];
			int new_y=ay+y_move[i];
			if(check(new_x,new_y,n,m)){
				dis[new_x][new_y]=1+dis[ax][ay];
				pair1.x=new_x;
				pair1.y=new_y;
				q[end1++]=pair1;
			}
		}
	}
}

int main(){
	int test;
	cin>>test;
	while(test--){
		int n,m;
		cin>>n>>m;
		int s_x,s_y,d_x,d_y;
		cin>>s_x>>s_y>>d_x>>d_y;
		for(int i=1;i<=n;i++)for(int j=1;j<=m;j++)cin>>matrix[i][j];
		for(int i=1;i<=n;i++)for(int j=1;j<=m;j++)dis[i][j]=-1;
		start1=0;
		end1=0;
		pair1.x=s_x;
		pair1.y=s_y;
		q[end1++]=pair1;
		int min1=0;
		calculate_bfs(d_x,d_y,n,m);
		for(int j=1;j<=m;j++)if(dis[1][j]>min1)min1=dis[1][j];
		cout<<min1<<endl;
	}
	return 0;
}
