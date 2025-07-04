### lsp-programs:

```c
//2. develop a c program to open an existing textfile and display its contents?
#include<stdio.h>
int main()
{
	FILE *file;
	char filename[100];
	char ch;
	printf("enter the filename to open:");
	scanf("%s",filename);
		file=fopen("text1.c","r");
	if(file==NULL)
	{
		printf("error:could not open file %s\n",filename);
		return 1;
	}
	printf("content of %s:\n\n",filename);
	while((ch=fgetc(file))!=EOF)
	{
		putchar(ch);
	}
	fclose(file);
	return 0;
	}
```

