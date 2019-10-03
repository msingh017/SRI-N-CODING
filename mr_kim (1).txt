#include<iostream>
using namespace std;

bool check(int visit[],int n){
	for(int i=0;i<n;i++)if(visit[i]==0)return false;
	return true;
}

void calculate(int sx,int sy,int pos,int dx,int dy,int n,int a[],int b[],int visit[],int value,int &min_dis){
	if(value>=min_dis)return;

	if(check(visit,n)){
		int disx,disy;
		if(pos!=-1){
			disx=dx-a[pos];
			disy=dy-b[pos];
			if(disx<0)disx=-disx;
			if(disy<0)disy=-disy;
		}
		else{
			disx=sx-dx;
			disy=sy-dy;
			if(disx<0)disx=-disx;
			if(disy<0)disy=-disy;
		}
		int sum = value + disx + disy;
		if(sum<min_dis)min_dis=sum;
		return;
	}

	for(int i=0;i<n;i++){
		if(visit[i]==0){
			visit[i]=1;
			int ss;
			if(pos==-1){
				int disx=sx-a[i];
				int disy=sy-b[i];
				if(disx<0)disx=-disx;
				if(disy<0)disy=-disy;
			 	ss = disx + disy;
				value+=ss;
			}
			else{
				int disx=a[pos]-a[i];
				int disy=b[pos]-b[i];
				if(disx<0)disx=-disx;
				if(disy<0)disy=-disy;
			 	ss = disx + disy;
				value+=ss;
			}
			calculate(sx,sy,i,dx,dy,n,a,b,visit,value,min_dis);
			visit[i]=0;
			value-=ss;
		}
	}
}


int main(){
	int test;
	cin>>test;
	while(test--){
		int n;
		cin>>n;
		int sx,sy,dx,dy;
		cin>>sx>>sy>>dx>>dy;
		int a[n],b[n];
		for(int i=0;i<n;i++)cin>>a[i]>>b[i];
		int min_dis=100001;
		int visit[n];
		for(int i=0;i<n;i++)visit[i]=0;
		calculate(sx,sy,-1,dx,dy,n,a,b,visit,0,min_dis);
		cout<<min_dis<<endl;
	}
	return 0;
}