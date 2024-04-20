# Encontrando Componentes Conexos em Grafos

## Introdução
Em teoria dos grafos, um **componente conexo** é um subconjunto de vértices e arestas em que cada vértice é acessível a partir de qualquer outro vértice no mesmo subconjunto, e não há conexões com vértices fora do subconjunto. Este documento explica como identificar componentes conexas em um grafo não direcionado usando o algoritmo de busca em profundidade (DFS).

## O Algoritmo DFS
O algoritmo de **busca em profundidade** (DFS, do inglês *Depth-First Search*) é uma técnica recursiva para percorrer todos os vértices e arestas de um grafo. A ideia básica é começar em um vértice, visitar um vizinho não visitado, e continuar esse processo até que não haja mais vizinhos não visitados. Em seguida, o algoritmo retrocede e repete o processo para outros vértices não visitados, encontrando assim todos os componentes conexas.

## Implementação
A implementação a seguir utiliza C++ e a Standard Template Library (STL) para representar o grafo e realizar a DFS.

### Estrutura do Grafo
O grafo é representado por uma lista de adjacência, onde cada vértice possui uma lista de seus vizinhos.

### Função DFS
A função `dfs` é chamada para cada vértice não visitado. Ela marca o vértice como visitado e, em seguida, chama recursivamente a si mesma para todos os vizinhos não visitados.

### Identificação de Componentes Conexos
Para identificar componentes conexas, a função `dfs` é chamada em um loop para cada vértice. Se o vértice não foi visitado, uma nova chamada `dfs` é iniciada, identificando assim um novo componente conexo.

## Código Completo

```cpp
#include<bits/stdc++.h>
using namespace std;

void dfs(int inicio, vector<vector<int>>& grafo, vector<bool> &no_visitado){
    no_visitado[inicio] = true;
    cout << inicio << " ";
    for(int visinho : grafo[inicio]){
        if(!no_visitado[visinho]){
            dfs(visinho, grafo, no_visitado);
        }
    }
}

int main()
{
    int num_nos, num_arestas;
    cin >> num_nos >> num_arestas;
    
    vector<vector<int>> grafo(num_nos);
    for(int i = 0; i < num_arestas; i++){
        int u, v; cin >> u >> v;
        grafo[u].push_back(v);
        grafo[v].push_back(u);
    }
    
    vector<bool> no_visitado(num_nos, false);
    for(int i = 0; i < num_nos; i++){
        if(!no_visitado[i]){
            dfs(i, grafo, no_visitado);
            cout << endl;
        }
    }
    return 0;
}
```

## Execução e Saída
Para executar o programa, compile-o com um compilador C++ e forneça o número de vértices e arestas, seguido pelas conexões entre os vértices. A saída será os componentes conexas do grafo, cada um listado em uma linha separada.

## Conclusão
Identificar componentes conexas é uma tarefa fundamental em muitos problemas de teoria dos grafos. A compreensão e implementação do algoritmo DFS são habilidades essenciais para qualquer pessoa interessada em algoritmos e estruturas de dados.
