
#include<stdio.h>
#include<malloc.h>
#include<stdlib.h>

typedef struct node
{
	int pno;
	struct node *link;
}NODE;

int noframes,noref,mat[10][20],frames[10];
NODE *first,*last;
NODE *getnode(int pno)
{
	NODE *t;
	t=(NODE *)malloc(sizeof(NODE));
	t->pno=pno;
	t->link=NULL;
}

void accept()
{
	int i,pno;
	NODE *p;
	printf("Enter No Of Frames: ");
	scanf("%d",&noframes);
	printf("Enter No Of References: ");
	scanf("%d",&noref);
	for(i=0;i<noref;i++)
	{
		printf("[%d]=",i);
		scanf("%d",&pno);
		p=getnode(pno);
		if(first==NULL)
		first=p;
		else
		last->link=p;
		last=p;
	}
}
	
int search(int pno)
{
	int i;
	for(i=0;i<noframes;i++)
	if(frames[i]==pno)
	return i;
	return -1;
}

void fifo()
{
	int i,j,sp=0,faults=0;
	NODE *p;
	for(i=0,p=first;i<noref;i++,p=p->link)
	{
		if(search(p->pno)==-1)
		{
		frames[sp]=p->pno;
		sp=(sp+1)%noframes;
		faults++;
		for(j=0;j<noframes;j++)
		mat[j][i]=frames[j];
		}
	}
for(p=first;p!=NULL;p=p->link)
printf("%3d",p->pno);
printf("\n\n");
for(j=0;j<noframes;j++)
{
	for(i=0;i<noref;i++)
	if (mat[j][i]!=0)
	printf("%3d",mat[j][i]);
	else
	
		printf("   ");
		printf("\n");
}
	printf("Total No Of Page Faults are= %d",faults);
}


int main() 
{
	accept();
	fifo();

}


