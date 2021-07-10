#include <stdio.h>
#include <stdlib.h>

struct node
{
    int data;
    struct node *next;
};

void create(struct node **);
void display(struct node *);
int survivor(struct node **, int);

int main()
{
    printf("********Josephus problem*********\n");
    struct node *l = NULL;//head
    int survive, skip;

    create(&l);
    printf("The persons in circular list are:\n");
    display(l);
    printf("Enter the number of persons to be skipped: ");
    scanf("%d", &skip);
    survive = survivor(&l, skip);
    printf("The person to survive is : %d\n", survive);
    free(l);

    return 0;
}

int survivor(struct node **l, int k)
{
    struct node *p, *q;
    int i;

    q = p = *l;
    while (p->next != p)
    {
        for (i = 0; i < k - 1; i++)
        {
            q = p;
            p = p->next;
        }
        q->next = p->next;
        printf("%d has been killed \n", p->data);
        free(p);
        p = q->next;
    }
    *l= p;

    return (p->data);
}
void create (struct node **l)
{
    struct node *q,*rear;
    int ele, ch;

    do
    {
        printf("Enter a number: ");
        scanf("%d", &ele);
        q= (struct node *)malloc(sizeof(struct node));
        q->data = ele;
        q->next = NULL;
        if (*l== NULL)
        {
            *l=q;
        }
        else
        {
            rear->next =q;
        }
        rear=q;
        printf("Do you want to add a number [1/0]? ");
        scanf("%d", &ch);
    } while (ch!= 0);
    rear->next = *l;
}

void display(struct node *l)
{
    struct node *q;//q means a temporary variable

    q= l;
    printf("%d-",q->data);
    q=q->next;
    while (l!=q)
    {
        printf("%d-",q->data);
        q=q->next;
    }
    printf("\n");
}
