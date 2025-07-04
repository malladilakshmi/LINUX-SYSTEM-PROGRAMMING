### LSP PROGRAMS:

### FILEMANAGEMENT:

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

```C
1.write a c program to create a new textfile and write "hello world" to it?
#include <stdio.h>

int main() {
    // Open the file in write mode
    FILE *file = fopen("text1.c", "w");

    // Check if the file was opened successfully
    if (file == NULL) {
        printf("Error opening file!\n");
        return 1;
    }

    // Write to the file
    fprintf(file, "Hello World");

    // Close the file
    fclose(file);

    printf("Data written to file successfully.\n");

    return 0;
}
/*************************************************************/
2. develop a c program to open an existing textfile and display its contents?
 #include<stdio.h>
int main()
{
        FILE *file;
        char filename[100];
        char ch;in 
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
/***************************************************************************************/
3.implement a c program to create a new directory named "test" in the current directory?
#include<stdio.h>
#include<sys/stat.h>
#include<sys/types.h>
int main()
{
        const char *dirname="test";
        int status=mkdir(dirname,0755);
        if(status==0)
        {
                printf("directory created successfully:%s\n",dirname);
        }
        else
        {
                perror("mkdir failed");
        }
        return 0;
}
/******************************************************************************************/
4.write a c program to check if a file named "sample.txt"exists in the current directory?                   
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
int main()
{
        FILE *file=fopen("sample.txt","r");
        if(file!=NULL)
        {
                printf("the file exits:");
        fclose(file);
        }
        else
        {
                printf("the file not exits:");
        }
        return 0;
}
/********************************************************************************************/
5.develop a c program to rename a file from "oldname.txt" to "newname.txt"?
#include<stdio.h>
int main()
{
        const char *oldname="text1.c",*newname="newname.txt";
        if(rename(oldname,newname)==0)
        {
                printf("file rename successfully\n");
        }
        else
        {
                perror("errorrenaming file");
        }
        return 0;
}

/*******************************************************************************************/
6.develop a c program to delete a file named "delete_me.txt?
#include<stdio.h>
int main()
{
                //const char *filename="delete_me.txt";
                int result=remove("delete_me.txt");
                if(result==0)
                {
                        printf("file is delete sucessfully");
                }
                else
                {
                        perror("error deleting file");
                }
                return 0;
}
/******************************************************************************************************/
7.write a c program to copy the contents of one file to another file?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        FILE *srcfile,*destfile;
        char srcfilename[]="source.txt";
        char destfilename[]="destination.txt";
        char ch;
        srcfile=fopen(srcfilename,"r");
        if(srcfile==NULL)
        {
                perror("error opening source file");
                return 1;
        }
        destfile=fopen(destfilename,"w");
        if(destfile==NULL)
        {
                perror("error opening destination file");
                fclose(srcfile);
                return 1;
                while((ch=fgetc(srcfile))!=EOF)
                {
                        putchar(ch);
                        fputc(ch,destfile);
                }
/*************************************************************************************************************/
8.develop a c program to move a file from one directory to another?
#include <stdio.h>

int main() {
    const char *source = "source_dir/file.txt";
    const char *destination = "destination_dir/file.txt";

    // Try to move (rename) the file
    if (rename(source, destination) == 0) {
        printf("File moved successfully.\n");
    } else {
        perror("Error moving file");
    }

    return 0;
}
/*************************************************************************************************************/
9.implement a c program to list all files in the current directory?
#include <stdio.h>
#include <dirent.h>

int main() {
    struct dirent *entry;
    DIR *dir = opendir(".");

    if (dir == NULL) {
        perror("Unable to open directory");
        return 1;
    }

    printf("Files and directories in the current directory:\n");
    while ((entry = readdir(dir)) != NULL) {
        printf("%s\n", entry->d_name);
    }

    closedir(dir);
    return 0;
}
/*******************************************************************************************************************/
10.write c program to get the size of a file named 'file.txt'?
#include <stdio.h>

int main() {
    FILE *file = fopen("file.txt", "rb");  // Open in binary read mode
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    // Seek to end of file
    fseek(file, 0, SEEK_END);

    // Get current file pointer position (which is the size)
    long size = ftell(file);
    if (size == -1L) {
        perror("Error getting file size");
        fclose(file);
        return 1;
    }

    printf("Size of 'file.txt': %ld bytes\n", size);

    fclose(file);
    return 0;
}
```
