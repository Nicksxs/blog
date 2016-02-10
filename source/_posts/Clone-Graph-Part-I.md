title: Clone Graph Part I
date: 2014-12-30 16:50:01
categories: leetcode
tags: [leetcode, C++]
---
### problem
``` 
Clone a graph. Input is a Node pointer. Return the Node pointer of the cloned graph.

A graph is defined below:
struct Node {
vector neighbors;
}
```

<!--more-->
### code

``` c++
typedef unordered_map<Node *, Node *> Map;
 
Node *clone(Node *graph) {
    if (!graph) return NULL;
 
    Map map;
    queue<Node *> q;
    q.push(graph);
 
    Node *graphCopy = new Node();
    map[graph] = graphCopy;
 
    while (!q.empty()) {
        Node *node = q.front();
        q.pop();
        int n = node->neighbors.size();
        for (int i = 0; i < n; i++) {
            Node *neighbor = node->neighbors[i];
            // no copy exists
            if (map.find(neighbor) == map.end()) {
                Node *p = new Node();
                map[node]->neighbors.push_back(p);
                map[neighbor] = p;
                q.push(neighbor);
            } else {     // a copy already exists
                map[node]->neighbors.push_back(map[neighbor]);
            }
        }
    }
 
    return graphCopy;
}
```
### anlysis
using the Breadth-first traversal
and use a map to save the neighbors not to be duplicated.

