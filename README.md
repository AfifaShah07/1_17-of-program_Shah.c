#include <stdio.h>
#include <stdlib.h>

#define MAX 20

// Adjacency List Node
struct Node {
    int data;
    struct Node* next;
};

struct Node* head[MAX]; // Graph
int visited[MAX];       // For DFS and BFS

// Function to add edge (Undirected Graph)
void addEdge(int u, int v) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = v;
    newNode->next = head[u];
    head[u] = newNode;

    // For undirected graph
    newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = u;
    newNode->next = head[v];
    head[v] = newNode;
}

// DFS Function
void DFS(int v) {
    visited[v] = 1;
    printf("%d ", v);

    struct Node* temp = head[v];
    while (temp != NULL) {
        if (!visited[temp->data]) {
            DFS(temp->data);
        }
        temp = temp->next;
    }
}

// BFS Function
void BFS(int start, int n) {
    int queue[MAX], front = 0, rear = 0;
    
    for (int i = 0; i < n; i++)
        visited[i] = 0;

    visited[start] = 1;
    queue[rear++] = start;

    while (front < rear) {
        int node = queue[front++];
        printf("%d ", node);

        struct Node* temp = head[node];
        while (temp != NULL) {
            if (!visited[temp->data]) {
                visited[temp->data] = 1;
                queue[rear++] = temp->data;
            }
            temp = temp->next;
        }
    }
}

int main() {
    int n, e;
    printf("Enter number of vertices: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++)
        head[i] = NULL;

    printf("Enter number of edges: ");
    scanf("%d", &e);

    printf("Enter edges (u v):\n");
    for (int i = 0; i < e; i++) {
        int u, v;
        scanf("%d %d", &u, &v);
        addEdge(u, v);
    }

    printf("\nDFS Traversal starting from node 0: ");
    for (int i = 0; i < n; i++)
        visited[i] = 0;
    DFS(0);

    printf("\nBFS Traversal starting from node 0: ");
    BFS(0, n);

    return 0;
}# 1_17-of-program_Shah.c
Printing BFS and DFS on graph
