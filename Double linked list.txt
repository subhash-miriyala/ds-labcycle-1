#include<stdio.h>
#include<stdlib.h>
struct node
{
    struct node *prev;
    struct node *next;
    int data;
};
struct node *l;//l=head
void main()
{
    int ch;
        printf("\n*******Double linked list********\n");
        struct node *create(struct node*);
        void insert_beg();
        void insert_last();
        void insert_pos();
        void delete_beg();
        void delete_last();
        void delete_pos();
        void display();
        void search();
        do
        {
        printf("\nChoose the following");
        printf("\n o.create a list\n 1.Insert in begining\n 2.Insert at last\n 3.Insert at any random location\n4.Delete from Beginning\n 5.Delete from last\n6.Delete the node after the given data\n7.Search\n8.Show\n9.Exit\n");
        printf("\nEnter your choice::");
        scanf("\n%d",&ch);
        switch(ch)
        {
            case 0:l=create(l);
            break;
            case 1:insert_beg();
            break;
            case 2:insert_last();
            break;
            case 3:insert_pos();
            break;
            case 4:delete_beg();
            break;
            case 5:delete_last();
            break;
            case 6:delete_pos();
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
                p->prev=NULL;
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
                        p->prev=q;
                 }
    }return l;
}
void insert_beg()
{
   struct node *p;
   int ele;
   p= (struct node *)malloc(sizeof(struct node));
   if(p==NULL)
   {
       printf("\nOVERFLOW");
   }
   else
   {
    printf("\nEnter element::");
    scanf("%d",&ele);

   if(l==NULL)
   {
       p->next = NULL;
       p->prev=NULL;
       p->data=ele;
       l=p;
   }
   else
   {
       p->data=ele;
       p->prev=NULL;
       p->next =l;
       l->prev=p;
       l=p;
   }
   printf("\nNode inserted\n");
}
}
void insert_last()
{
   struct node *p,*q;
   int ele;
   p = (struct node *) malloc(sizeof(struct node));
   if(l==NULL)
    l=p;
   if(p == NULL)
   {
       printf("\nOVERFLOW");
   }
   else
   {
       printf("\nEnter value::");
       scanf("%d",&ele);
        p->data=ele;
       if(l == NULL)
       {
           p->next = NULL;
           p->prev = NULL;
           l = p;
       }
       else
       {
          q = l;
          while(q->next!=NULL)
          {
              q = q->next;
          }
          q->next = p;
          p->prev=q;
          p->next = NULL;
          }
       printf("\nnode inserted\n");
   }
}
void insert_pos()
{
   struct node *p,*q;
   int ele,pos,i;
   p= (struct node *)malloc(sizeof(struct node));
   if(p == NULL)
       printf("\n OVERFLOW");
   else
   {
       q=l;
       printf("Enter the position");
       scanf("%d",&pos);
       for(i=0;i<pos;i++)
       {
           q = q->next;
           if(q == NULL)
           {
               printf("\n There are less than %d elements", pos);
               return;
           }
       }
       printf("Enter value");
       scanf("%d",&ele);
       p->data = ele;
       p->next = q->next;
       p -> prev = q;
       q->next = p;
       q->next->prev=p;
       printf("\n node inserted");
   }
}
void delete_beg()
{
    struct node *p;
    if(l == NULL)
    {
        printf("\n UNDERFLOW");
    }
    else
    {
        p = l;
        l = l -> next;
        l -> prev = NULL;
        free(p);
        printf("\n node deleted");
    }

}
void delete_last()
{
    struct node *p;
    if(l == NULL)
    {
        printf("\n UNDERFLOW");
    }
    else
    {
        p = l;
        while(p->next!= NULL)
            p = p -> next;
        p -> prev -> next = NULL;
        free(p);
        p=NULL;
        printf("\n node deleted");
    }
}
void delete_pos()
{
    struct node *p, *q;
    int ele;
    printf("\n after the node to be deleted : ");
    scanf("%d", &ele);
    p = l;
    while(p -> data!= ele)
    p = p-> next;
    if(p -> next == NULL)
    {
        printf("\n Node not to be delete");
    }
    else
    {
        q = p -> next;
        p -> next = q -> next;
        q -> next -> prev = p;
        free(q);
        printf("\nnode deleted");
    }
}
void display()
{
    struct node *p;
    p = l;
    if(l == NULL)
    {
        printf("Nothing to print");
    }
    else
    {
        printf("printing values:");
        while (p!=NULL)
        {
            printf("%d->",p->data);
            p = p -> next;
        }
    }printf("NULL\n");
}
void search()
{
    struct node *p;
    int ele,i=0,flag;
    p = l;
    if(p == NULL)
    {
        printf("\nEmpty List");
    }
    else
    {
        printf("\nEnter item which you want to search:");
        scanf("%d",&ele);
        while (p!=NULL)
        {
            if(p->data == ele)
            {
                printf("\nelement found at position %d :",i+1);
                flag=0;
                break;
            }
            else
            {
                flag=1;

            }
            i++;
            p = p -> next;
        }
        if(flag==1)
        {
            printf("\nItem not found\n");
        }
    }
}
