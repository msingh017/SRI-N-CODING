#include<iostream>
using namespace std;
int a[13][5];
int b[5][5];

void change(int i){
	for(int j=i;j>(i-5);j--){
		for(int k=0;k<5;k++){
			if(j>=0 && a[j][k]==2){
				a[j][k]=0;
				b[i-j][k]=2;
			}
		}
	}
}

void rechange(int i){
	for(int j=i;j>(i-5);j--){
		for(int k=0;k<5;k++){
			if(j>=0 && b[i-j][k]==2){
				a[j][k]=2;
				b[i-j][k]=0;
			}
		}
	}
}


void find_max(int pos,int n,int count,int &max1_sum){
	if(pos<0 || pos>4 || count<0 || n<0)return;
	if(n==0){
		if(count>max1_sum)max1_sum=count;
		return;
	}
	if(a[n-1][pos]==1)count++;
	else if(a[n-1][pos]==2)count--;
	else{
		find_max(pos,n-1,count,max1_sum);
		find_max(pos+1,n-1,count,max1_sum);
		find_max(pos-1,n-1,count,max1_sum);
	}
}

int main(){
	int test;
	cin>>test;
	while(test--){
		int n;
		cin>>n;
		for(int i=0;i<n;i++)for(int j=0;j<5;j++)cin>>a[i][j];
		for(int i=0;i<5;i++)a[n][i]=0;
		int start1=n-1;
		int max1_sum=-1;
		for(int i=n-1;i>=0;i--){
			change(i);
			find_max(2,n+1,0,max1_sum);
			rechange(i);
		}
		cout<<max1_sum<<endl;
	}
	return 0;
}
