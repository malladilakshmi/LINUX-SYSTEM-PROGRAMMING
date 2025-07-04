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

```

