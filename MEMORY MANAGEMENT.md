### MEMORY MANAGEMENT:

```c
1. Write a C program to demonstrate dynamic memory allocation using malloc()?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        int *arr;
        int n=5,i;
        arr=(int*)malloc(n*sizeof(int));//dynamically allocate memory using malloc()
        if(arr==NULL)
        {
                printf("memory alloction failed!\n");
                return 1;
        }
        printf("enter %d integer :\n",n);
        for(i=0;i<n;i++)
        {
                printf("element %d:",i+1);
                scanf("%d",&arr[i]);
        }
        printf("you entered:\n");
        for(i=0;i<n;i++)
        {
                printf("%d",arr[i]);
        }
                        printf("\n");
        free(arr);//free the allocate memory
        return 0;
}
/**********************************************************************************************************************************************************/
2. Implement a C program to allocate memory for an array dynamically using calloc().
#include<stdio.h>
#include<stdlib.h>
int main()
{
        int *arr;
        int n,i;
        printf("enter the number of elements:");
        scanf("%d",&n);
        arr=(int *)calloc(n,sizeof(int));
        if(arr==NULL)
        {
                printf("memory allocation failed!\n");
                return 1;
        }
        printf("\n");
        printf("enter %d integers:\n",n);
        for(i=0;i<n;i++)
        {
                printf("element %d:",i+1);
                scanf("%d",&arr[i]);
        }
        printf("you entered:\n");
        for(i=0;i<n;i++)
        {
        printf("%d",arr[i]);
        }
        free(arr);
        return 0;
}
/***************************************************************************************************************************/
//3. Write a C program to resize dynamically allocated memory using realloc
#include<stdio.h>
#include<stdlib.h>
int main()
{
        int *arr;
        int i,n,newsize;
        printf("enter the number of elements:");
        scanf("%d",&n);
        arr=(int*)malloc(n*sizeof(int));
        if(arr==NULL)
        {
                printf("memory allocation failed!\n");
                return 1;
        }
        printf("enter %d integers:\n");
        for(i=0;i<n;i++)
        {
                printf("element %d:",i+1);
                scanf("%d",&arr[i]);
        }
        printf("enter the new size of the array:");
        scanf("%d",&newsize);
        int *temp=(int*)realloc(arr,newsize*sizeof(int));
        if(temp==NULL)
        {
                printf("memory reallocation failed!\n");
                free(arr);
                return 1;
        }
        arr=temp;
        if(newsize>n)
        {
                for(i=n;i<newsize;i++)
                {
                        arr[i]=0;
                }
                               }
        }
        printf("array after resizing:\n");
        for(i=0;i<newsize;i++)
        {
                printf("%d",arr[i]);
        }
        printf("\n");
        free(arr);
        return 0;
}

/************************************************************************************************************************/

```

