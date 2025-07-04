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

```C12.write a c program to create a new directory named "backup" in the parent directory? 
#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>

int main() {
    const char *dir_path = "./Backup";

    // Create the directory with read/write/execute permissions for the user
    if (mkdir(dir_path, 0755) == 0) {
        printf("Directory 'Backup' created successfully in the parent directory.\n");
    } else {
        perror("Error creating directory");
    }

    return 0;
}
/**************************************************************************************************************************/
//13. Write a C program to recursively list all files and directories in a given directory?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>
#include <errno.h>

void list_directory(const char *path, int level) {
    DIR *dir;
    struct dirent *entry;

    if (!(dir = opendir(path))) {
        perror("opendir");
        return;
    }

    while ((entry = readdir(dir)) != NULL) {
        // Skip "." and ".."
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;

        char full_path[4096];
        snprintf(full_path, sizeof(full_path), "%s/%s", path, entry->d_name);

        struct stat st;
        if (stat(full_path, &st) == -1) {
            perror("stat");
            continue;
        }

        // Print indentation
        for (int i = 0; i < level; i++) {
            printf("  ");
        }

/*************************************************************************************************************************/
14. Develop a C program to delete all files in a directory named "Temp"?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <unistd.h>

int main() {
    DIR *dir;
    struct dirent *entry;
    char path[1024];

    // Open the "Temp" directory
    dir = opendir("Temp");
    if (dir == NULL) {
        perror("Unable to open Temp directory");
        return 1;
    }

    // Loop through all entries
    while ((entry = readdir(dir)) != NULL) {
        // Skip "." and ".."
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;

        // Build full file path
        snprintf(path, sizeof(path), "Temp/%s", entry->d_name);

        // Delete the file
        if (remove(path) == 0) {
            printf("Deleted: %s\n", path);
        } else {
            perror("Failed to delete file");
        }
    }

    closedir(dir);
    return 0;
}
/*********************************************************************************************************/
15.Implement a C program to count the number of lines in a file named "data.txt"?
#include <stdio.h>

int main() {
    FILE *file;
    char ch;
    int lines = 0;

    // Open the file in read mode
    file = fopen("data.txt", "r");

    // Check if file opened successfully
    if (file == NULL) {
        perror("Unable to open file");
        return 1;
    }

    // Count lines by reading each character
    while ((ch = fgetc(file)) != EOF) {
        if (ch == '\n') {
            lines++;
        }
    }

    // Close the file
    fclose(file);

    // If file is not empty, count last line if it doesn't end with \n
    if (lines == 0 && ch != EOF) {
        lines = 1;
    }

    // Print the result
    printf("Number of lines in data.txt: %d\n", lines);

    return 0;
}
/********************************************************************************************************/
16. Write a C program to append "Goodbye!" to the end of an existing file 
named "message.txt"?
#include <stdio.h>

int main() {
    FILE *file;

    // Open the file in append mode
    file = fopen("message.txt", "a");

    // Check if file opened successfully
    if (file == NULL) {
        perror("Unable to open file");
        return 1;
    }

    // Append the text
    fprintf(file, "Goodbye!");

    // Close the file
    fclose(file);

    printf("Text appended successfully to message.txt\n");

    return 0;
}
/**************************************************************************************************************/
17.Implement a C program to change the permissions of a file named 
"file.txt" to read only?
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>

int main() {
    const char *filename = "file.txt";

    // Set permissions to read-only for owner, group, and others
    if (chmod(filename, S_IRUSR | S_IRGRP | S_IROTH) == 0) {
        printf("Permissions changed: %s is now read-only.\n", filename);
    } else {
        perror("Failed to change permissions");
        return 1;
    }

    return 0;
}
**************************************************************************************************************/
18.Write a C program to change the ownership of a file named "file.txt" to 
the user "user?
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pwd.h>
#include <sys/types.h>
#include <errno.h>

int main() {
    const char *filename = "file.txt";
    const char *new_owner = "user";

    // Get user information
    struct passwd *pw = getpwnam(new_owner);
    if (pw == NULL) {
        perror("User not found");
        return 1;
    }

    // Change ownership of the file
    if (chown(filename, pw->pw_uid, -1) == -1) {
        perror("chown failed");
        return 1;
    }

    printf("Ownership of '%s' changed to user '%s' (UID: %d).\n", filename, new_owner, pw->pw_uid);
    return 0;
/***********************************************************************************************************************/
19.Implement a C program to create a temporary file and write some data 
toit?
#include <stdio.h>
#include <stdlib.h>
int main() {
    FILE *tempFile;
    char tempFileName[L_tmpnam];

    // Generate a unique temporary filename
    tmpnam(tempFileName);

    // Open the temporary file for writing
    tempFile = fopen(tempFileName, "w+");  // "w+" means read/write
    if (tempFile == NULL) {
        perror("Failed to create temporary file");
        return 1;
    }

    // Write some data to the file
    fprintf(tempFile, "This is some temporary data.\nLine 2 of data.\n");

    // Rewind the file to read what was written
    rewind(tempFile);

    // Read and print the content
    char ch;
    printf("Contents of temporary file (%s):\n", tempFileName);
    while ((ch = fgetc(tempFile)) != EOF) {
        putchar(ch);
    }

    // Close and delete the file
    fclose(tempFile);
    remove(tempFileName);  // Clean up the temporary file

    return 0;
}
/*************************************************************************************************************/
20. Develop a C program to get the last modified timestamp of a file named "file.txt"?
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <time.h>

int main() {
    const char *filename = "file.txt";
    struct stat fileStat;

    if (stat(filename, &fileStat) == -1) {
        perror("Error getting file information");
        return 1;
    }

    printf("Last modified time of '%s': %s", filename, ctime(&fileStat.st_mtime));

    return 0;
}
/*******************************************************************************************************************/
21.Write a C program to check if a given path refers to a file or a 
directory?
#include<stdio.h>
#include<sys/stat.h>
#include<stdlib.h>
int main()
{
        char path[256]="/home";
        struct stat path_stat;
        if(stat(path,&path_stat)!=0)
                        {
                        perror("stat");
                        return 0;
                        }
        if(S_ISDIR(path_stat.st_mode))
        {
                printf("%s is a directory.\n",path);
        }
        else
        {
                printf("%s is neither a regular file nor a directory.\n",path);
        }
return 0;
}
/*******************************************************************************************************************/
22.Develop a C program to create a hard link named "hardlink.txt" to a file 
named
"source.txt"?
#include<stdio.h>
#include<unistd.h>
int main()
{
        const char *source="source.txt";
        const char *linkname="hardlink.txt";
        if(link(source,linkname)==0)
        {
                printf("hardlink %s created succesfully for %s\n",linkname,source);
        }
        else
        {
                perror("error creating hardlink");
        }
        return 0;
}
/******************************************************************************************************************/
22.Develop a C program to create a hard link named "hardlink.txt" to a file 
named
#include<stdio.h>
#include<stdlib.h>
int main()
{
        FILE *file;
        char line[1024];
        file=fopen("data.csv","r");
        if(file==NULL)
        {
                printf("error opening file");
                return 1;
        }
        printf("contents of data.csv\n");
        while(fgets(line,sizeof(line),file))
        {
                printf("%s",line);
        }
        fclose(file);
        return 0;
}
/*************************************************************************************************************/
24.Write a C program to get the absolute path of the current working directory?
#include<stdio.h>
#include<unistd.h>
#include<limits.h>
int main()
{
        char path[256];
        if(getcwd(path,sizeof(path))!=NULL)
        {
                printf("current working directory:%s\n",path);
        }
        else
        {
        perror("getcwd(),error");
        return 1;
}
return 0;
}
/**************************************************************************************************************/
25. Develop a C program to get the size of a directory named "Documents"?
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <sys/stat.h>
#include <string.h>

#define DIRECTORY "Documents"

long long get_directory_size(const char *path) {
    struct dirent *entry;
    struct stat statbuf;
    char fullpath[1024];
    long long total_size = 0;

    DIR *dir = opendir(path);
    if (dir == NULL) {
        perror("opendir");
        return -1;
    }

    while ((entry = readdir(dir)) != NULL) {
        // Skip "." and ".."
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;

        snprintf(fullpath, sizeof(fullpath), "%s/%s", path, entry->d_name);

        if (stat(fullpath, &statbuf) == -1) {
            perror("stat");
            continue;
        }

        // If it's a file, add size
        if (S_ISREG(statbuf.st_mode)) {
            total_size += statbuf.st_size;
        }

        // Optionally, recurse into subdirectories
        else if (S_ISDIR(statbuf.st_mode)) {
            total_size += get_directory_size(fullpath);
        }
    }

    closedir(dir);
    return total_size;
}

int main() {
    long long size = get_directory_size(DIRECTORY);
    if (size >= 0) {
        printf("Total size of '%s' directory: %lld bytes\n", DIRECTORY, size);
    }
    return 0;
}
/*******************************************************************************************************/
26.Implement a C program to recursively copy all files and directories from one directory
to another?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <dirent.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <fcntl.h>
#include <errno.h>

#define BUFFER_SIZE 4096

void copy_file(const char *src_path, const char *dest_path) {
    int src_fd = open(src_path, O_RDONLY);
    if (src_fd < 0) {
        perror("open source file");
        return;
    }

    int dest_fd = open(dest_path, O_WRONLY | O_CREAT | O_TRUNC, 0644);
    if (dest_fd < 0) {
        perror("open destination file");
        close(src_fd);
        return;
    }

    char buffer[BUFFER_SIZE];
    ssize_t bytes_read, bytes_written;

    while ((bytes_read = read(src_fd, buffer, BUFFER_SIZE)) > 0) {
        bytes_written = write(dest_fd, buffer, bytes_read);
        if (bytes_written != bytes_read) {
            perror("write error");
            break;
        }
    }

    close(src_fd);
    close(dest_fd);
}

void copy_directory(const char *src_dir, const char *dest_dir) {
    DIR *dir = opendir(src_dir);
    if (!dir) {
        perror("opendir");
        return;
    }

    struct dirent *entry;
    struct stat statbuf;

    mkdir(dest_dir, 0755); // create destination directory

    while ((entry = readdir(dir)) != NULL) {
        // Skip "." and ".."
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;

        char src_path[PATH_MAX];
        char dest_path[PATH_MAX];

        snprintf(src_path, PATH_MAX, "%s/%s", src_dir, entry->d_name);
        snprintf(dest_path, PATH_MAX, "%s/%s", dest_dir, entry->d_name);

        if (stat(src_path, &statbuf) == -1) {
            perror("stat");
            continue;
        }

        if (S_ISDIR(statbuf.st_mode)) {
            // Recurse into subdirectory
            copy_directory(src_path, dest_path);
        } else if (S_ISREG(statbuf.st_mode)) {
            // Copy regular file
            copy_file(src_path, dest_path);
        }
    }

    closedir(dir);
}

int main(int argc, char *argv[]) {
    if (argc != 3) {
        fprintf(stderr, "Usage: %s <source_directory> <destination_directory>\n", argv[0]);
        return 1;
    }

    struct stat statbuf;
    if (stat(argv[1], &statbuf) == -1 || !S_ISDIR(statbuf.st_mode)) {
        fprintf(stderr, "Source must be a valid directory\n");
        return 1;
    }

    copy_directory(argv[1], argv[2]);

    printf("Directory copied from %s to %s\n", argv[1], argv[2]);
    return 0;
}
/********************************************************************************************************/
27.Write a C program to get the number of files in a directory named "Images"?
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <sys/stat.h>
#include <string.h>

int main() {
    const char *folder_name = "Images";
    DIR *dir = opendir(folder_name);

    if (dir == NULL) {
        perror("Could not open directory 'Images'");
        return EXIT_FAILURE;
    }

    struct dirent *entry;
    struct stat entry_stat;
    int file_count = 0;
    char path[1024];

    while ((entry = readdir(dir)) != NULL) {
        // Skip . and ..
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;

        snprintf(path, sizeof(path), "%s/%s", folder_name, entry->d_name);
        if (stat(path, &entry_stat) == 0 && S_ISREG(entry_stat.st_mode)) {
            file_count++;
        }
    }

    closedir(dir);

    printf("Number of files in '%s': %d\n", folder_name, file_count);

    return EXIT_SUCCESS;
}
/***********************************************************************************************************/
28.Develop a C program to create a FIFO (named pipe) named "myfifo" in the current
directory?
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <errno.h>

int main() {
    const char *fifo_path = "myfifo";

    // Create the FIFO with read-write permissions (0666)
    if (mkfifo(fifo_path, 0666) == -1) {
        if (errno == EEXIST) {
            printf("FIFO '%s' already exists.\n", fifo_path);
        } else {
            perror("mkfifo");
            return EXIT_FAILURE;
        }
    } else {
        printf("FIFO '%s' created successfully.\n", fifo_path);
    }

    return EXIT_SUCCESS;
}
/**************************************************************************************************************/
29.Implement a C program to read data from a FIFO named "myfifo"?#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>

#define FIFO_NAME "myfifo"
#define BUFFER_SIZE 1024

int main() {
    char buffer[BUFFER_SIZE];
    int fd;

    // Open the FIFO for reading
    fd = open(FIFO_NAME, O_RDONLY);
    if (fd == -1) {
        perror("Failed to open FIFO for reading");
        return EXIT_FAILURE;
    }

    printf("Reading from FIFO '%s'...\n", FIFO_NAME);

    // Read data from the FIFO
    ssize_t bytes_read;
    while ((bytes_read = read(fd, buffer, sizeof(buffer) - 1)) > 0) {
        buffer[bytes_read] = '\0'; // Null-terminate the string
        printf("Received: %s\n", buffer);
    }

    if (bytes_read == -1) {
        perror("Read error");
    } else {
        printf("EOF reached. No more writers.\n");
    }

    close(fd);
    return EXIT_SUCCESS;
}
```

