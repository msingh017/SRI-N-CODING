#include<iostream>
using namespace std;
int a[21][21];
int visit[21][21];
int x_move[]={-1,0,1,0};
int y_move[]={0,1,0,-1};

struct queue1{
	int ax;
	int ay;
};

queue1 q1[400];
int start1,end1;

bool check(int x1,int x2,int n){
	if(x1<1 || x2<1 || x1>n || x2>n || visit[x1][x2]!=-1 || a[x1][x2]!=1)return false;
	return true;
}

void calculate_dis(int pos_x,int pos_y,int n){
	start1=0;
	end1=0;
	queue1 q2;
	q2.ax=pos_x;
	q2.ay=pos_y;
	q1[end1++]=q2;
	visit[pos_x][pos_y]=0;
	while(start1!=end1){
		int x1=q1[start1].ax;
		int y1=q1[start1].ay;
		start1++;
		for(int i=0;i<4;i++){
			int new_x=x1+x_move[i];
			int new_y=y1+y_move[i];
			if(check(new_x,new_y,n)){
				visit[new_x][new_y]=1+visit[x1][y1];
				q2.ax=new_x;
				q2.ay=new_y;
				q1[end1++]=q2;
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
		int x[m];
		int y[m];
		for(int i=0;i<m;i++)cin>>x[i]>>y[i];
		for(int i=1;i<=n;i++)for(int j=1;j<=n;j++)cin>>a[i][j];
		int max_dis=-1;
		for(int i=1;i<=n;i++){
			for(int j=1;j<=n;j++){
				if(a[i][j]==1){
					for(int k=1;k<=n;k++)for(int k1=1;k1<=n;k1++)visit[k][k1]=-1;
					calculate_dis(i,j,n);
					int count=0;
					for(int k=0;k<m;k++){
						if(visit[x[k]][y[k]]!=-1){
							if(count<visit[x[k]][y[k]])count=visit[x[k]][y[k]];
						}
						else{
							count=-1;
							break;
						}
					}
					if(count==-1)max_dis=-1;
					else if(max_dis==-1)max_dis=count;
					else if(max_dis>count)max_dis=count;
				}
			}
		}
		cout<<max_dis<<endl;
	}
	return 0;
}