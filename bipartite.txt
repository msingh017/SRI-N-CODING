#include<iostream>
using namespace std;
#define ll long long int

struct Node{
	ll val;
	Node *next;
};

Node *q[100001];
ll a[100001];     //queue array
ll start1,end1;

Node *get_node(ll data){
	Node *new_node = new Node();
	new_node->val = data;
	new_node->next = NULL;
	return new_node;
}

Node *insert1(ll x,ll data){
	Node *ptr;
	if(q[x]==NULL)q[x]=get_node(data);
	else{
		ptr=get_node(data);
		ptr->next=q[x];
		q[x]=ptr;
	}
	return q[x];
}

bool bfs(ll i,ll color[],ll n){
	start1=0,end1=0;
	color[i]=1;
	ll check=1;
	a[end1++]=i;
	while(start1!=end1){
		ll t1=a[start1++];
		Node *ptr=q[t1];
		while(ptr!=NULL){
			if(t1==ptr->val)return false;
			if(color[ptr->val]==-1){
				color[ptr->val]=1-color[t1];
				a[end1++]=ptr->val;
			}
			else if(color[ptr->val]==color[t1])return false;
			ptr=ptr->next;
		}
	}
	return true;
}

int main(){
	ll test;
	cin>>test;
	while(test--){
		ll n,m;
		cin>>n>>m;
		for(ll i=0;i<=n;i++)q[i]=NULL;
		ll x,y;
		while(m--){
			cin>>x>>y;
			q[x]=insert1(x,y);
			q[y]=insert1(y,x);
		}
		ll color[n+1];
		for(ll i=0;i<=n;i++)color[i]=-1;
		int flag=true;
		for(ll i=1;i<=n;i++){
			if(color[i]==-1){
				if(bfs(i,color,n)==false){
					flag=false;
					break;
				}
			}
		}
		if(flag){
			ll count=0;
			for(ll i=1;i<=n;i++)if(color[i]==1)count++;
			cout<<count<<endl;
			for(ll i=1;i<=n;i++)if(color[i]==1)cout<<i<<" ";
			cout<<endl;
		}
		else cout<<"-1"<<endl;
	}
	return 0;
}