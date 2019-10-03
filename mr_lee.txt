#include<iostream>
using namespace std;
int matrix[100][100];
int visit[100];

bool check(int n){
	for(int i=0;i<n;i++){
		if(visit[i]==0)return false;
	}
	return true;
}

void calculate(int n,int pos,int sum,int &min_dis){
	if(check(n)){
		int sum1=matrix[pos][0];
		sum1+=sum;
		if(sum1<min_dis)min_dis=sum1;
		return;
	}
	for(int i=0;i<n;i++){
		if(!visit[i]){
			visit[i]=1;
			calculate(n,i,sum+matrix[pos][i],min_dis);
			visit[i]=0;
		}
	}
}

int main(){
	int test;
	cin>>test;
	while(test--){
		int n;
		cin>>n;
		for(int i=0;i<n;i++)for(int j=0;j<n;j++)cin>>matrix[i][j];
		for(int i=0;i<n;i++)visit[i]=0;
		int min_dis=100001;
		calculate(n,0,0,min_dis);
		if(min_dis==100001)cout<<"0"<<endl;
		else cout<<min_dis<<endl;
	}
	return 0;
}