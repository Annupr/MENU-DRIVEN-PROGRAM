# MENU-DRIVEN-PROGRAM
Here is the program to insert and delete a menu driven program
#include<stdio.h>
#include<stdlib.h>

struct Node{
	int data;
	struct Node *next;
};
void first(struct Node ** head_ref,int new_data)
{	//allocate a node
	struct Node* new_node = (struct Node*)malloc(sizeof(struct Node*));
	 // put in the data
	 new_node->data=new_data;
	 //make next of new node is head
	 new_node->next=(*head_ref);
	 (*head_ref)=new_node;
}
void last(struct Node ** head_ref,int new_data)
{
	printf("in last\n");
	struct Node *ptr=*head_ref;
	struct Node *new_node = (struct Node*)malloc(sizeof(struct Node*));
	
		new_node->data=new_data;
		new_node->next=NULL;
		if(*head_ref==NULL){
			*head_ref=new_node;
			return;
		}


	while(ptr->next!=NULL){
			ptr=ptr->next;
	}
	ptr->next=new_node;
	return;
}
void middle(struct Node *head_ref,int new_data)
{
	int flag=0;
	struct Node *ptr=NULL;
	ptr=head_ref;
	int ele;
	printf("\nEnter the element after which you want to insert\n");
	scanf("%d",&ele);
	//printf(" head = %d"*prev_node);
	/*if(prev_node==NULL)
	{
		printf("\nPrevious node cannot be null.");
		return;
	}*/
	while(ptr->next!=NULL)
	{	
		if(ptr->data==ele)
		{
		//	printf("found");
		struct Node* new_node = (struct Node*)malloc(sizeof(struct Node*));
		new_node->data=new_data;
		new_node->next=ptr->next;
		ptr->next=new_node;
			flag=0;
		return;
		}
		else{
			flag++;
		}
			ptr=ptr->next;
	}
		if(flag!=0)
		{
			printf("\nelement not found");
		}
}
void printList(struct Node *node)
{	
	while(node!=NULL)
	{
		printf("%d ",node->data);
		node=node->next;
	}
	printf("\n ____________________________________________________________________________________\n");
}
void delete_ele(struct Node **head_ref,int ele){
	struct Node *temp=*head_ref;
	struct Node *prev;
	if(temp!=NULL&&temp->data==ele)//for first element
	{
		*head_ref=temp->next;
		free(temp);
		return;
	}
	while(temp!=NULL&&temp->data!=ele){
		prev=temp;
		temp=temp->next;
		//printf("in while");
	}
	if(temp==NULL)
	{
		printf("link list is empty\n pls tey insering some elements\n");
		return;
	}
	prev->next=temp->next;
	free(temp);
}

 

int main()
{
	int op,c=0,ele;
	struct Node *head=NULL;
	while(c==0){
		printf("\nSelect \n1 to insert at the begining:\n2 to insert in the middle :\n3to insert at the end:\n4 to print: \n5 to delete an element from begining \n and any other number to exit :\n ");
		scanf("%d",&op);
		switch(op){
					case 1:
							printf("\n Enter the element to be inserted:\n");
							scanf("%d",&ele);
							first(&head,ele);//&head is passed
							printList(head);
							break;
					case 2:
							printf("\n Enter the element to be inserted:\n");
							scanf("%d",&ele);
							middle(head,ele);//head is passed
							printList(head);
							break;		
					case 3:
							printf("\n Enter the element to be inserted:\n");
							scanf("%d",&ele);
							last(&head,ele);
							printList(head);
							break;	
					case 4:
							printf("\n the link list is :\n"); 
							printList(head);
							break; 
					case 5:
							printf("\n Enter the element you want to delete:\n");
							scanf("%d",&ele);
							delete_ele(&head,ele);
							printList(head);
							break;	
					default: c=1;
							printf("\nPress any key to exit....\n");
		}
	}
}
