# Topological-sort

Topological sort

#include <iostream>
  
#include <stack>
  
#include <vector>
  
#include <list>
  
using namespace std;

vector <int> order;
  
void find_id(list<int> g[],int id[],int n){  //寻找入度,没有使用
  
	int i;
  
	list<int>::iterator k;
  
	for(i=0;i<n;i++){
  
		for(k=g[i].begin();k!=g[i].end();k++){
    
			id[*k]++;
      
		}
    
	}
  
}

void topo(list<int> g[],int id[],int n,bool &OK,bool &incon){//OK==false 表示未确定顺序 incon==true 表示发现矛盾
  
	stack<int> s;
  
	order.erase(order.begin(),order.end());
  
	int t[26];
  
	copy(&id[0],&id[n],&t[0]);
  
	int i;
  
	for(i=0;i<n;i++){
  
		if(id[i]==0) 
    
			s.push(i);
      
	}
  
	if(s.size()!=1) OK=false;
  
	int count=0;
  
  
	while(!s.empty()){
  
		int v=s.top(); s.pop(); count++;
    
		order.push_back(v);
    
		list<int>::iterator k;
    
		for(k=g[v].begin();k!=g[v].end();k++){
    
			id[*k]--;
      
			if(id[*k]==0) s.push(*k);
      
			if(s.size()>1) OK=false;
      
		}
    
	}
  
	if(order.size() < n) OK=false;   //矛盾发生,会导致这种情况,小心
  
	if(count < n) incon=true;
  
	copy(&t[0],&t[n],&id[0]);
  
}
