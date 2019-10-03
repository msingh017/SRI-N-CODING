#include<iostream>
using namespace std;
#define ll long long int 

ll a[1000][1000];
ll dp[1000][1000];

ll max1(ll num1,ll num2){
	return num1>num2 ? num1:num2;
}

ll findmaxsum(int n,int m){
	dp[n-1][m-1]=a[n-1][m-1]; //bottom right remains same as it is
	for(int i=m-2;i>=0;i--)dp[n-1][i]=a[n-1][i]+dp[n-1][i+1];  //filling last row
	for(int i=n-2;i>=0;i--)dp[i][m-1]=a[i][m-1]+dp[i+1][m-1];  //filling last column
	for(int i=n-2;i>=0;i--){			//filling rest of the rows and columns
		for(int j=m-2;j>=0;j--){
			ll t=max1(dp[i+1][j],dp[i][j+1]);
			dp[i][j]=a[i][j]+t;
		}
	}
	return dp[0][0];
}

int main()
{
	int t;
	cin>>t;
	while(t--){
		int n,m;
		cin>>n>>m;
		for(int i=0;i<n;i++)for(int j=0;j<m;j++)cin>>a[i][j];
		ll cal=findmaxsum(n,m);
		cout<<cal<<endl;
	}
	return 0;
}