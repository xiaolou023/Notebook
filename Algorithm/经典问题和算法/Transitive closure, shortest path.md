# Transitive closure/ shortest path

**Floyd–Warshall algorithm**

```
for(k=1;k<=n;k++) // for each intermediate node
 for(i=1;i<=n;i++) // for each start node
  for(j=1;j<=n;j++) // for each end note
    if(dist[i][k]+dist[k][j]<dist[i][j])
      dist[i][j]=dist[i][k]+dist[k][j];
```

