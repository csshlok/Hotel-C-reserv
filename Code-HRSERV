#include<stdio.h>
#include<conio.h>
#include<string.h>
#include<stdlib.h>
//defining the structure
struct node
{
int room;
struct node *left ;
struct node *right;
char fname[50];
char lname[50];
char regno[50];
};
//global variables
int a[100];
int counter=0;
/*to allot a room*/
struct node* insert(int troom,char tfname[],char tlname[],char treg[],struct node* root)
{
	struct node *temp1=NULL;
	struct node *temp2=NULL;
	struct node *p=NULL;
    p=(struct node *)malloc(sizeof(struct node));
    p->room=troom;
    strcpy(p->fname,tfname);
    strcpy(p->regno,treg);
    strcpy(p->lname,tlname);
    p->left=p->right=NULL;
    if(root==NULL)
    root=p;
    else
     {
        temp1=root;
        while(temp1!=NULL)
        {
        	temp2=temp1;
        	if(p->room<temp1->room)
        	temp1=temp1->left;
        	else
        	temp1=temp1->right;
        }
        if(temp1==NULL)
        {
        	if(p->room<temp2->room)
        	temp2->left=p;
        	else
        	temp2->right=p;
        }
        printf("\n Alloted successfully.\n");
     }
    return root;
}
/* to create a new allotment*/
struct node *create(struct node *root)
{
	int troom;
	do
	{
    printf("Choose the rooms between 1-100 <if you don't want to choose press 0>\n ");
    scanf("%d",&troom);
    if(troom!=0)
    {
    if(a[troom-1]==1)
    	printf("This room is occupied. \nKindly choose another room. \n ");
    else
    {
    	char tfname[50];char treg[50];char tlname[50];
        printf("Enter student's first name : ");
        scanf("%s",tfname);
        printf("Enter student's last name : ");
        scanf("%s",tlname);
        printf("Enter the students registration number : ");
        scanf("%s",treg);
        a[troom-1]=1;
        counter++;
        root=insert(troom,tfname,tlname,treg,root);
        printf("\nSuccessfully alloted.\n");
    }
    }
    }while(troom!=0);
    
    return(root);
}
/*to get the total no. of rooms alloted*/
void rfilled()
{
printf("The total number of rooms alloted are : %d \n",counter);
}
/*deletion of a particular room*/
struct node *del(int n, struct node *root)
{
	struct node *temp1=NULL;//temp1 to traverse the tree
	struct node *temp2=NULL;//temp2 to traverse the parent
	struct node *p=NULL;
	int val;
	temp1=root;
	while(n!=temp1->room)
	{
		temp2=temp1;
		if(n<temp1->room)
		temp1=temp1->left;//traversing the left subtree
		else
		temp1=temp1->right;//traversing the right subtree
		if(temp1==NULL)
		break;
	}//after its completion temp1 will point to the data to be deleted and temp2 to its parent
	if(temp1==NULL)
	printf("\nThe room you are searching for isn't alloted yet.\n");
	else
	{
		p=temp1;
/*deletion in the case where the node has no nodes*/
		if(p->left==NULL&&p->right==NULL)
		{

			if(temp2==NULL)
			printf("\nDeleting the allotment...\n");
			else
			{
				if(temp2->left==p)
                temp2->left=NULL;
				if(temp2->right==p)
				temp2->right=NULL;
				free(p);
		}
		}
/*deletion in the case where the node has one daughter node*/
		else if(p->left==NULL||p->right==NULL)
		{
			printf("\nDeleting room number : %d",p->room);
			if(p->left!=NULL)
			{
				if(temp2==NULL)
				root=p->left;//deleting root with only left subtree
				else
				{
				if(temp2->left==p)
				temp2->left=p->left;
				if(temp2->right==p)
				temp2->right=p->left;
			    }
			}
			if(p->right!=NULL)
			{
				if(temp2==NULL)
				root=p->right;//deleting root with only right subtree
				else
				{
				if(temp2->left==p)
				temp2->left=p->right;
				if(temp2->right==p)
				temp2->right=p->right;
		        }
			}
			free(p);
		}
/*deletion in the case where the node has two daughter nodes*/
		else if(p->left!=NULL && p->right!=NULL)
		{
			printf("\nDeleting the room number : %d",p->room);
			temp1=p->right;
			while(temp1->left!=NULL)
			temp1=temp1->left;//temp1 now points to the least value in the right subtree of node p
			val=temp1->room;
			del(val,root);//recursive call
			p->room=val;
		}
		printf("\nDeletion Successfull.\n");
	}
	counter--;
	return(root);
}
/*to search for a particular node*/
void search1(int x,struct node * root)
{
	struct node *q=root;
	while(x!=q->room)
	{
		if(x<q->room)
		q=q->left;
		else
		q=q->right;
		if(q==NULL)
		break;
	}
	if(q!=NULL)
	{
		printf("\nName of the student:- %s %s\n",q->fname,q->lname);
		printf("Registration no.:- %s\n",q->regno);
	}
	else
	printf("\nThat room isn't alloted yet.\n");
}
/*to sort the tree and display it*/
int inorder(struct node *root)
{
	if(root==NULL)
	{
		printf("\nNo record found.\n");
		return 0;
	}
	if(root->left!=NULL)
	inorder(root->left);
	printf("%d",root->room);
	printf("\t\t%s",root->fname);
	printf("\t\t%s",root->lname);
	printf("\t\t%s",root->regno);
	printf("\n");
	if(root->right!=NULL)
	inorder(root->right);
	return 0;
}
void main()
{
	struct node *root=NULL;
     int i;
     int ch;
   
	do
	{
	  int s, ch, t;
	  menu :	//label for goto(used later)
	 printf("What do you want to do? \n 1. Allot a room \n 2. Delete an alloted room\n 3. View all the alloted rooms along with the student details \n 4. To search any particular room \n 5. View the number of rooms alloted \n 6. Exit\t : ");
		scanf("%d",&s);
		switch(s)
         {
            case 1:
        	    root=create(root);
        	    break;
            case 2:
            	printf("\nEnter the room number to be deleted : ");
        	    scanf("%d",&ch);
        	    root=del(ch,root);
        	    break;
            case 3:
	            printf("ROOM NO. \t FIRST NAME \t LAST NAME \t REG NO.\n");
            	inorder(root);
            	break;
        	case 4:
        	    printf("\nEnter the room no. : ");
        	    scanf("%d",&t);
        	    search1(t,root);
        	    break;
        	case 5:
        	    rfilled();
        	    break;
        	case 6 : 
        		exit(0);
        	default : 
        		printf("Invalid choice.");
         }
     printf("Enter 1 to go back to the menu.\t : ");
     scanf("%d",&ch);
     if(ch==1)
     	goto menu;	//using the label "menu" as mentioned above
	}while(ch==1);
}
