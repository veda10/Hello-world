#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#define N  4
int space = 0;
int openNodes = 0;
int closedNodes = 0;
typedef struct node{

	int A[N][N];
	struct node * parent;
	struct node* next;
	int level;
	int pathCost;
	int x_cor;
	int y_cor;
	
	
}NODE;
typedef struct queue {
	NODE *qnode;
	int pathcost;
	struct queue *next;
} QUEUE;

void swap(int *x,int *y){
	
	int temp = *x;
	*x = *y;
	*y = temp;
	
}

QUEUE *openQueue = NULL;
QUEUE *closedQueue = NULL;

int row[] = {1,0,-1,0};
int col[] = {0,-1,0,1};
/* Inserting an element at the rear of the queue - FIFO */
QUEUE *insertQueue(QUEUE *queue,NODE *node) {
	QUEUE *front = queue, *rear , *temp;
	int pc;
	rear = (QUEUE *)malloc(sizeof(QUEUE));
	rear->qnode = node;    //added this line
	rear->next = NULL;
	//rear->pathcost=pc;	//commented this line and making writing a new line 
	rear->pathcost = rear->qnode->pathCost;
	if (queue == NULL) return rear;

	if(queue->pathcost > rear->pathcost)
	{
		rear->next=queue;
		return rear;
	}
	
	while(queue->next != NULL) {
	
	if(queue->pathcost > rear->pathcost){
		rear->next=queue;
		temp->next=rear;
		return front;
	}
	temp=queue;
	queue = queue->next;
	}

	if(queue->pathcost > rear->pathcost)
	{
		rear->next=queue;
		temp->next=rear;
	}
	else{
	queue->next = rear;}
	
	return front;
}

//extractmin
QUEUE *extractmin(QUEUE *queue) {
	
	if (queue == NULL) return queue;
	QUEUE *temp = NULL;
	temp = queue;
//printf("&&\n");
	return temp;
}

/* Delete the element at front of the QUEUE - FIFO */
QUEUE *deleteQueue(QUEUE *queue) {
	if (queue == NULL) return queue;
	QUEUE *temp = NULL;
	temp = queue;
	queue = queue->next;
	free(temp);
	//printf("%p\n",queue);
	return queue;
}

/*Checks If The list is Empty Or Not*/
int check(QUEUE *queue){

	if(queue == NULL) return 0;
	else return 1;

}

/*Checks For A VAlid Move*/
int boundaryCheck(int a,int b){

	if(a>=0 && a < N && b >= 0 && b < N){
	
		return 1;
	}
	else return 0;


}
/*int getcals(QUEUE *queue){
	int counter = 0;
	while(queue){
		
		counter +=1;
		queue=queue->next;
	}
return counter;
}*/

void printMatrix(int matrix[][N]){

	int i,j;
	for(i=0;i<N;i++)
	{
		for(j=0;j<N;j++)
		{
			printf("%d ",matrix[i][j]);
		}
		printf("\n");
	}

	

}

void printPath(NODE* node){

	if(node == NULL)
		return;
	
	printPath(node->parent);
	printMatrix(node->A);

	printf("\n");


}

NODE* newNODE(int initial[][N],int x,int y,int newX,int newY,int level,NODE *parent){

	NODE *root = (NODE*)malloc(sizeof(NODE));
	root->parent = parent;
	
	int i,j;
	for(i = 0;i<N;i++)
	{
		for(j=0;j<N;j++)
		{
			root->A[i][j] = initial[i][j];
		}
	}
	root->level = level;
	root->x_cor = newX;
	root->y_cor = newY;

	swap(&root->A[x][y],&root->A[newX][newY]);

	

return root;
}

/*Heuristic-1*/
int mismatchcount(int X[][N],int Y[][N])
{
    int count=0;
    int i,j;
    for(i=0;i<N;i++)
    {
        for(j=0;j<N;j++)
        {
            if(X[i][j]!=Y[i][j])
            {
            count++;
            }
        }
    }
return count;
}

int getInvCount(int arr[])
{
    int inv_count = 0;
    for (int i = 0; i < N * N - 1; i++)
    {
        for (int j = i + 1; j < N * N; j++)
        {
            // count pairs(i, j) such that i appears
            // before j, but i > j.
            if (arr[j] && arr[i] && arr[i] > arr[j])
                inv_count++;
        }
    }
    return inv_count;
}

// find Position of blank from bottom
int findXPosition(int puzzle[N][N])
{
    // start from bottom-right corner of matrix
    for (int i = N - 1; i >= 0; i--)
        for (int j = N - 1; j >= 0; j--)
            if (puzzle[i][j] == 0)
                return N - i;
}

int isSolvable(int puzzle[N][N])
{
    // Count inversions in given puzzle
    int invCount = getInvCount((int*)puzzle);
 
    // If grid is odd, return true if inversion
    // count is even.
    if (N & 1)
        return !(invCount & 1);
 
    else     // grid is even
    {
        int pos = findXPosition(puzzle);
        if (pos & 1)
            return !(invCount & 1);
        else
            return invCount & 1;
    }
}

/*Delete Element From The Middle*/
QUEUE *deleteinmiddle(QUEUE *queue,NODE *node){
	if (queue == NULL) return queue;
	QUEUE *temp1 = NULL,*front=queue;
	if(queue->qnode->pathCost==node->pathCost)
	{
	queue=queue->next;
	return queue;
	}
	else
	{
	while(queue->next!=NULL)
	{
		if(queue->qnode->pathCost==node->pathCost)
		{
			temp1->next=queue->next;
			return front;
		}
		temp1=queue;
		queue=queue->next;
	}
		if(queue->qnode->pathCost==node->pathCost)
		{
			temp1->next=NULL;
		}
	
	}

return front;
}

int compareMatrix(int X[][N],int Y[][N])
{
	int i,j;
	for(i=0;i<N;i++)
	{
		for(j=0;j<N;j++)
		{
			if(X[i][j]!=Y[i][j])
			{
				return 1;
			}
		}
	}

return 0;

}

int searchInQueue(NODE * child,QUEUE *closed)
{
	
	int z;
	QUEUE * temp;
	temp = closed;
	while(closed!=NULL)
	{
		z=compareMatrix(child->A,closed->qnode->A);
		if(z==0)
		{
			if(child->pathCost > closed->qnode->pathCost){
				
				return 0;
			}
			else if(child->pathCost < closed->qnode->pathCost){
				
								
				closed=deleteinmiddle(temp,closed->qnode);
				
				return 2;
			}
		
		}
		
		closed=closed->next;
	}
return 1;
}



void searchState(int start[][N],int goal[][N],int x,int y){
	
	/*Make New NOde*/

	NODE *node = newNODE(start,x,y,x,y,0,NULL);
	space = space + 1;	

	int i,j;
	

	openQueue = insertQueue(openQueue,node);
	openNodes += 1;
	
	/*while The Open List IS Not Empty*/	
	while (check(openQueue)==1){
		
		NODE *closeNode = extractmin(openQueue)->qnode;
			
		closedQueue = insertQueue(closedQueue,closeNode);
		closedNodes += 1;
		openQueue=deleteQueue(openQueue);
		openNodes -= 1;		
		
		if(mismatchcount(closeNode->A,goal)==0)
		{	
			printf("PATH\n");
			printPath(closeNode);
			//getcals(openQueue);
			return;

		}
		
		for(i=0;i<4;i++)
		{
			
			if(boundaryCheck(closeNode->x_cor+row[i],closeNode->y_cor+col[i])==1){
					
				 NODE* childNode = newNODE(closeNode->A, closeNode->x_cor,
                              	 closeNode->y_cor, closeNode->x_cor + row[i],
                                 closeNode->y_cor + col[i],
                              	 closeNode->level + 1, closeNode);
				 int heur_1 = mismatchcount(childNode->A,goal);
				 childNode->pathCost =childNode->level + heur_1; 
				 space += 1;
				
				/*Check For Duplicates  in the closedList*/
				int closedFlag = searchInQueue(childNode,closedQueue);
				if(closedFlag==0)
				{
					
					free(childNode);
					continue;
				}
				else if(closedFlag==2)
				{
					
					openQueue=insertQueue(openQueue,childNode);
					openNodes += 1;
					closedNodes -= 1;
				}
				

				/*Check For Duplicates  in the openList*/
				int openFlag=searchInQueue(childNode,openQueue);
				if(openFlag==0)
				{
					
					free(childNode);
					continue;
				}
				else if(openFlag==2)
				{
					
					openQueue=insertQueue(openQueue,childNode);
					//openNodes += 1;

				}					
				else if(openFlag==1)
				{
	
					openQueue = insertQueue(openQueue,childNode);
					openNodes += 1;
				
				}
				
			}
		}	
	
	}
			
}


int main(){
	clock_t t;
	t = clock();
	int i,j;
	

	int initial[4][4] = 
	{
		{1,2,3,4},
		{5,6,7,8},
		{11,12,0,15},
		{10,9,13,14}

	};

	int initial2[4][4] = 
	{
		{0,1,2,3},
		{5,6,7,4},
		{9,10,11,8},
		{13,14,15,12}

	};


	int Final[4][4] = 
	{
		{1,2,3,4},
		{5,6,7,8},
		{9,10,11,12},
		{13,14,15,0}

	};
	int initital2[3][3]=
	{
		{1,2,3},
		{5,6,0},
		{7,8,4}
	};
	//Unsolvable Case
	int puzzle[N][N] = {
					{3, 9, 1, 15},
					{14, 11, 4, 6},
					{13, 0, 10, 12},
					{2, 7, 8, 5},
				};
	int FInal[3][3]=
	{
		{1,2,3},
		{4,5,6},
		{7,8,0}};
	
	
	int x = 2; //initial x-position of zero
	int y = 2; //initial y-position of zero

	/*Checks If The Problem Is Solvable Or Unsolvable*/
	int solvable = isSolvable(initial);
	if(solvable == 1)
	{
		
		searchState(initial,Final,x,y);
		printf("Solved\n");
		
		printf("Total number of generated nodes:%d\n",space);
		printf("Total number of generated nodes in Open List:%d\n",openNodes);
		printf("Total number of generated nodes in Closed List:%d\n",closedNodes);
	}
	else
	{
		printf("The given puzzle is Unsolvable\n");
	}	

	t = clock() - t;
	double time_taken = ((double)t)/CLOCKS_PER_SEC;
	printf("Time Taken %f seconds to execute\n",time_taken);	
return 0;
}
