#include<stdio.h>
#include<stdlib.h>
struct node
{
    int data;
    struct node *next;
};
struct node *l=NULL;//l=head (starting node);

int main()
{
        struct node *create(struct node*);
        void insert_beg();
        void insert_last ();
        void insert_middle();
        void delete_beg();
        void delete_last();
        void delete_mid();
        void display();
        void search();
int ch;
    do
    {
        printf("*******Single Linked List********\n\n");
        printf("...Choose the following...\n");
        printf("\n 0.create a nodes\n 1.Insert in begining \n 2.Insert at last\n 3.Insert at any position\n 4.Delete from Beginning\n 5.Delete from last\n 6.Delete node after specified position\n 7.Search for an element\n 8.Show\n 9.Exit\n");
        printf("\nEnter your choice?\n");
        scanf("\n%d",&ch);
        switch(ch)
        {
            case 0:l=create(l);
            break;
            case 1:insert_beg();
            break;
            case 2:insert_last();
            break;
            case 3:insert_mid();
            break;
            case 4:delete_beg();
            break;
            case 5:delete_last();
            break;
            case 6:delete_mid();
            break;
            case 7:search();
            break;
            case 8:display();
            break;
            case 9:exit(0);
            break;
            default:printf("Please enter valid choice..");
        }

    }while(ch<=9);
}
struct node *create(struct node *l)
{
     int i,n,ele;
     struct node *p,*q;//p=new node,q=which helps a traversing the next node
     printf("enter no.of nodes:");
     scanf("%d",&n);
     for(i=0;i<n;i++)
    {
                printf("Enter Data:");
                scanf("%d",&ele);
                p=(struct node*)malloc(sizeof(struct node));
                p->data=ele;
                p->next=NULL;
                if(l==NULL)
                {
                        l=p;
                }
                else
                {
                    q=l;
                    while(q->next!=NULL)
                       q = q->next;
                        q->next=p;
                 }
    }return l;
}
void insert_beg()
{
    struct node *p;
    int ele;
        if(l == NULL)
    {
        l=p;
    }
    else
    {
        printf("\nEnter value\n");
        scanf("%d",&ele);
         p = (struct node *) malloc(sizeof(struct node *));
        p->data = ele;
        p->next = l;
        l= p;
        printf("\nNode inserted");
    }

}
void insert_last()
{
    struct node *p,*q;
    int ele;
    p = (struct node*)malloc(sizeof(struct node));
    if(p == NULL)
    {
        printf("\nOVERFLOW");
    }
    else
    {
        printf("\nEnter value?\n");
        scanf("%d",& ele);
        p->data = ele;
        if(l== NULL)
        {
            p-> next = NULL;
            l = p;
            printf("\nNode inserted");
        }
        else
        {
            q = l;
            while (q -> next != NULL)
            {
                q = q -> next;
            }
            q->next = p;
            p->next = NULL;
            printf("\nNode inserted");

        }
    }
}
void insert_mid()
{
    int i,pos,ele;
    struct node *p, *q;
    p = (struct node *) malloc (sizeof(struct node));
    if(p == NULL)
    {
        printf("\nOVERFLOW");
    }
    else
    {
        printf("\nEnter element value");
        scanf("%d",&ele);
        p->data = ele;
        printf("\nEnter the position after which you want to insert ");
        scanf("\n%d",&pos);
        q=l;
        for(i=0;i<pos;i++)
        {
            q = q->next;
            if(q == NULL)
            {
                printf("\ncan't insert\n");
                return;
            }

        }
        p->next = q ->next;
        q ->next = p;
        printf("\nNode inserted");
    }
}
void delete_beg()
{
    struct node *p;
    if(l == NULL)
    {
        printf("\nList is empty\n");
    }
    else
    {
        p= l;
        l = p->next;
        free(p);
        printf("\nNode deleted from the begining ...\n");
    }
}
void delete_last()
{
    struct node *p,*q;
    if(l == NULL)
    {
        printf("\nlist is empty");
    }
    else if(l -> next == NULL)
    {
        l = NULL;
        free(l);
        printf("\nOnly node of the list deleted ...\n");
    }

    else
    {
        p = l;
        while(p->next != NULL)
        {
            q = p;
            p = p ->next;
        }
        q->next = NULL;
        free(p);
        printf("\nDeleted Node from the last ...\n");
    }
}
void delete_mid()
{
     struct node *p, *q;
   int ele;
      printf("\n Enter the element which you have deleted :");
      scanf("%d", &ele);
      p = l;
   while(p->data!=ele)
     {
      q = p;
      p = p -> next;
     }
      q -> next = p -> next;
      free(p);
      return l;
}
void search()
{
    struct node *p;
    int ele,i=0,flag;
    p = l;
    if(p== NULL)
    {
        printf("\nEmpty List\n");
    }
    else
    {
        printf("\nEnter item which you want to search:");
        scanf("%d",&ele);
        while (p!=NULL)
        {
            if(p->data == ele)
            {
                printf("item found at position %d ",i+1);
                flag=0;
                break;
            }
            else
            {
                flag=1;
            }
            i++;
            p = p-> next;
        }
        if(flag==1)
        {
            printf("Item not found\n");
        }
    }

}
void display()
{
    struct node *p;
    p = l;
    if(p == NULL)
    {
        printf("Nothing to print");
    }
    else
    {
        printf("printing values:");
        while (p!=NULL)
        {
            printf("\n%d",p->data);
            p = p -> next;
        }
    }
}

