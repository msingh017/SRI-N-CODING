#include<iostream>
using namespace std;
bool dp[100][10000];
int index;
int subset_array[100];

void fill_dp_table(int a[],int n,int size){
	for(int i=0;i<=size;i++){			//fill first row
		if(a[0]==i)dp[0][i]=true;
		else dp[0][i]=false;
	}
	for(int i=1;i<n;i++){				//fill rest of the table
		for(int j=0;j<=size;j++){
			if(j<a[i])dp[i][j]=dp[i-1][j];
			else if(a[i]==j)dp[i][j]=true;
			else dp[i][j]=dp[i-1][j] | dp[i-1][j-a[i]];
		}
	}
}
void find_subset_array(int a[],int row,int sum){
	while(sum!=-1 && row>=0){
		if(sum==a[row] && dp[row][sum]==true){
			sum=-1;
			subset_array[index++]=a[row];
		}
		else if(row-1>=0 && sum-a[row]>=0 && dp[row-1][sum-a[row]]==true){
			sum=sum-a[row];
			subset_array[index++]=a[row];
			row--;
		}
		else row--;
	}
}

int main(){
	int test;
	cin>>test;
	for(int t=1;t<=test;t++){
		int n;
		cin>>n;
		int a[n],sum=0;
		for(int i=0;i<n;i++){
			cin>>a[i];
			sum+=a[i];
		}
		int size_sum=sum/2;
		fill_dp_table(a,n,size_sum);

		// for(int i=0;i<n;i++){
		// 	for(int j=0;j<=size_sum;j++)cout<<dp[i][j]<<" ";
		// 	cout<<endl;
		// }

		int result=-1;
		int copy1[n];
		for(int i1=size_sum;i1>=0;i1--){
			if(n-2>=0 && dp[n-1][i1]==true && dp[n-2][i1]==true){
				index=0;
				for(int i=0;i<n;i++)copy1[i]=a[i];
				find_subset_array(a,n-1,i1);
				
				for(int i=0;i<index;i++){
					for(int j=0;j<n;j++){
						if(subset_array[i]==copy1[j]){
							copy1[j]=-1;
							break;
						}
					}
				}
				
			  	// cout<<"sum="<<i1<<endl;
				// for(int i=0;i<index;i++)cout<<subset_array[i]<<" ";
				// cout<<endl;

				for(int j1=n-2;j1>=0;j1--){
					if(dp[j1][i1]==true){
						index=0;
						find_subset_array(a,j1,i1);

						int flag=false;
						for(int i=0;i<index;i++){
							flag=false;
							for(int j=0;j<n;j++){
								if(subset_array[i]==copy1[j]){
									flag=true;
									break;
								}
							}
							if(flag==false)break;
						}
						if(flag)result=i1;

						// for(int i=0;i<index;i++)cout<<subset_array[i]<<" ";
						// cout<<endl;

					}
					if(result!=-1)break;
				}
			}
			if(result!=-1)break;
		}
		if(result==-1)result=0;
		cout<<"#"<<t<<" "<<result<<endl;
	}
	return 0;
}