### LSP PROGRAMS:

### FILEMANAGEMENT:

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

```C

12.write a c program to create a new directory named "backup" in the parent directory? 
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

```C
30.Write a C program to truncate a file named "file.txt" to a specified length?
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <errno.h>

int main() {
    const char *filename = "file.txt";
    off_t new_length;

    // Prompt the user for the new length
    printf("Enter new length for '%s': ", filename);
    if (scanf("%ld", &new_length) != 1 || new_length < 0) {
        fprintf(stderr, "Invalid length. Please enter a non-negative number.\n");
        return EXIT_FAILURE;
    }

    // Try truncating the file
    if (truncate(filename, new_length) == -1) {
        perror("Error truncating file");
        return EXIT_FAILURE;
    }

    printf("File '%s' truncated to %ld bytes successfully.\n", filename, (long)new_length);
    return EXIT_SUCCESS;
}
/***********************************************************************************************************************/
31.Develop a C program to search for a specific string in a file named "data.txt" and
display the line number(s) where it occurs?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_LINE 1024

int main() {
    FILE *file;
    char line[MAX_LINE];
    char search[100];
    int line_num = 0;
    int found = 0;

    // Ask user for the search string
    printf("Enter the string to search: ");
    if (fgets(search, sizeof(search), stdin) == NULL) {
        fprintf(stderr, "Error reading input.\n");
        return EXIT_FAILURE;
    }

    // Remove newline character from search string
    search[strcspn(search, "\n")] = '\0';

    // Open file
    file = fopen("data.txt", "r");
    if (file == NULL) {
        perror("Failed to open data.txt");
        return EXIT_FAILURE;
    }

    // Read file line by line
    while (fgets(line, sizeof(line), file)) {
        line_num++;
        if (strstr(line, search)) {
            printf("Found on line %d: %s", line_num, line);
            found = 1;
        }
    }

    if (!found) {
        printf("The string '%s' was not found in the file.\n", search);
    }

    fclose(file);
    return EXIT_SUCCESS;
}
/************************************************************************************************************/
32.Implement a C program to get the file type (regular file, directory, symbolic link, etc.) of
a given path?
// file_type.c
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <unistd.h>
#include<string.h>
void print_file_type(const char *path) {
    struct stat st;

    // Use lstat to avoid dereferencing symbolic links
    if (lstat(path, &st) == -1) {
        perror("lstat");
        return;
    }

    // Determine file type using macros
    printf("File type of '%s': ", path);
    if (S_ISREG(st.st_mode))
        printf("Regular file\n");
    else if (S_ISDIR(st.st_mode))
        printf("Directory\n");
    else if (S_ISLNK(st.st_mode))
        printf("Symbolic link\n");
    else if (S_ISCHR(st.st_mode))
        printf("Character device\n");
    else if (S_ISBLK(st.st_mode))
        printf("Block device\n");
    else if (S_ISFIFO(st.st_mode))
        printf("FIFO (named pipe)\n");
    else if (S_ISSOCK(st.st_mode))
        printf("Socket\n");
    else
        printf("Unknown\n");
}

int main() {
    char path[1024];

    printf("Enter path to check: ");
    if (fgets(path, sizeof(path), stdin) == NULL) {
        fprintf(stderr, "Error reading path.\n");
        return EXIT_FAILURE;
    }

    // Remove newline from input
    path[strcspn(path, "\n")] = '\0';

    print_file_type(path);
    return EXIT_SUCCESS;
}
/***************************************************************************************************************/
33.Write a C program to create a new empty file named "empty.txt"? write only access?
// create_empty_file.c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
    const char *filename = "empty.txt";

    // Open the file with write-only and create flags, set permissions to 0644
    int fd = open(filename, O_WRONLY | O_CREAT | O_TRUNC, 0644);
    if (fd == -1) {
        perror("Failed to create file");
        return EXIT_FAILURE;
    }

    printf("File '%s' created successfully.\n", filename);

    close(fd);
    return EXIT_SUCCESS;
}
    open()
    A system call that opens a file and returns a file descriptor.
    filename
    A const char* that points to the name of the file (e.g., "empty.txt").
    O_WRONLY
    Open the file for write-only access.
O_CREAT
    If the file does not exist, it will be created.
    O_TRUNC
    If the file already exists, its content will be truncated to 0 bytes (i.e., emptied).
    0644
    This is the file permission:
        Owner can read/write (6)
        Group can read (4)
        Others can read (4)

    Note: This third argument (0644) is only used when the file is created (i.e., when O_CREAT is set.
/**************************************************************************************************************/
33a.Write a C program to create a new empty file named "empty.txt"?using read only access?
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
    const char *filename = "empty.txt";

    int fd = open(filename, O_RDONLY);
    if (fd == -1) {
        perror("Failed to open file for reading");
        return 1;
    }

    printf("File '%s' opened in read-only mode.\n", filename);

    close(fd);
    return 0;
}
/*************************************************************************************************************/
34. Develop a C program to get the permissions (mode) of a file named "file.txt"?
// file_permissions.c
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <unistd.h>

void print_permissions(mode_t mode) {
    printf("Permissions: ");

    // Owner
    printf((mode & S_IRUSR) ? "r" : "-");
    printf((mode & S_IWUSR) ? "w" : "-");
    printf((mode & S_IXUSR) ? "x" : "-");

    // Group
    printf((mode & S_IRGRP) ? "r" : "-");
    printf((mode & S_IWGRP) ? "w" : "-");
    printf((mode & S_IXGRP) ? "x" : "-");

    // Others
    printf((mode & S_IROTH) ? "r" : "-");
    printf((mode & S_IWOTH) ? "w" : "-");
    printf((mode & S_IXOTH) ? "x" : "-");

    printf("\n");
}

int main() {
    const char *filename = "file.txt";
    struct stat st;

    // Get file status
    if (stat(filename, &st) == -1) {
        perror("stat");
        return EXIT_FAILURE;
    }

    printf("File: %s\n", filename);
    print_permissions(st.st_mode);

    return EXIT_SUCCESS;
}
/***************************************************************************************************/
35.Implement a C program to recursively delete a directory named "Temp" and all its
contents?
// delete_directory.c
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>
#include <string.h>
#include <errno.h>

int delete_directory(const char *path) {
    DIR *dir = opendir(path);
    if (!dir) {
        perror("opendir");
        return -1;
    }

    struct dirent *entry;
    char full_path[PATH_MAX];

    while ((entry = readdir(dir)) != NULL) {
        // Skip "." and ".."
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;

        snprintf(full_path, sizeof(full_path), "%s/%s", path, entry->d_name);

        struct stat st;
        if (lstat(full_path, &st) == -1) {
            perror("lstat");
            closedir(dir);
            return -1;
        }

        if (S_ISDIR(st.st_mode)) {
            // Recursive call for subdirectory
            if (delete_directory(full_path) == -1) {
                closedir(dir);
                return -1;
            }
        } else {
            // Delete file or symlink
            if (unlink(full_path) == -1) {
                perror("unlink");
                closedir(dir);
                return -1;
            }
        }
    }

    closedir(dir);

    // Remove the now-empty directory
    if (rmdir(path) == -1) {
        perror("rmdir");
        return -1;
    }

    return 0;
}

int main() {
    const char *target = "Temp";

    if (delete_directory(target) == 0) {
        printf("Directory '%s' deleted successfully.\n", target);
    } else {
        printf("Failed to delete directory '%s'.\n", target);
    }

    return 0;
}
/***************************************************************************************************************/
36.Write a C program to read and display the first 10 lines of a file named "log.txt"?
// read_first_10_lines.c
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *fp = fopen("log.txt", "r");
    if (fp == NULL) {
        perror("Failed to open log.txt");
        return 1;
    }

    char line[1024];
    int count = 0;

    while (fgets(line, sizeof(line), fp) != NULL && count < 10) {
        printf("%s", line);  // Print the line
        count++;
    }

    if (count == 0) {
        printf("log.txt is empty or has no readable lines.\n");
    }

    fclose(fp);
    return 0;
}
/**********************************************************************************************************************/
37.Develop a C program to read data from a text file named "input.txt" and write it to
another file named "output.txt" in reverse order?
// reverse_file.c
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *fin = fopen("input.txt", "r");
    if (fin == NULL) {
        perror("Failed to open input.txt");
        return 1;
    }

    FILE *fout = fopen("output.txt", "w");
    if (fout == NULL) {
        perror("Failed to open output.txt");
        fclose(fin);
        return 1;
    }

    // Move to the end of the file to get size
    fseek(fin, 0, SEEK_END);
    long size = ftell(fin);

    // Read characters in reverse
    for (long i = size - 1; i >= 0; i--) {
        fseek(fin, i, SEEK_SET);
        int ch = fgetc(fin);
        fputc(ch, fout);
    }

    printf("Reversed content written to output.txt\n");

    fclose(fin);
    fclose(fout);
    return 0;
}
/***********************************************************************************************/
38.Implement a C program to create a new directory named with the current date in the
format "YYYY-MM-DD"?
// create_date_directory.c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <sys/stat.h>
#include <string.h>
#include <errno.h>

int main() {
    char dirname[11]; // "YYYY-MM-DD" + '\0'

    // Get current date
    time_t now = time(NULL);
    struct tm *t = localtime(&now);

    // Format date as YYYY-MM-DD
    strftime(dirname, sizeof(dirname), "%Y-%m-%d", t);

    // Create directory
    if (mkdir(dirname, 0755) == -1) {
        if (errno == EEXIST) {
            printf("Directory '%s' already exists.\n", dirname);
        } else {
            perror("mkdir failed");
            return 1;
        }
    } else {
        printf("Directory '%s' created successfully.\n", dirname);
    }

    return 0;
}
/***************************************************************************************************/
39. Write a C program to read and display the contents of a binary file named "binary.bin"?
// read_binary_file.c
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *fp = fopen("binary.bin", "rb");
    if (fp == NULL) {
        perror("Failed to open binary.bin");
        return 1;
    }

    unsigned char byte;
    int count = 0;

    printf("Contents of binary.bin (in hex):\n");

    while (fread(&byte, sizeof(unsigned char), 1, fp) == 1) {
        printf("%02X ", byte);
        count++;

        // Print 16 bytes per line
        if (count % 16 == 0) {
            printf("\n");
        }
    }

    if (count % 16 != 0) {
        printf("\n");
    }

    fclose(fp);
    return 0;
}
/**********************************************************************************************/
40.Develop a C program to get the size of the largest file in a directory?
// largest_file_size.c
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <sys/stat.h>
#include <string.h>

int main() {
    const char *dirname = "."; // Change to desired directory, e.g., "Files"
    DIR *dir = opendir(dirname);
    if (dir == NULL) {
        perror("opendir failed");
        return 1;
    }

    struct dirent *entry;
    struct stat file_stat;
    char fullpath[PATH_MAX];
    off_t max_size = 0;
    char largest_file[PATH_MAX] = "";

    while ((entry = readdir(dir)) != NULL) {
        // Skip "." and ".."
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;

        // Create full path to file
        snprintf(fullpath, sizeof(fullpath), "%s/%s", dirname, entry->d_name);

        // Get file stats
        if (stat(fullpath, &file_stat) == -1)
            continue;

        // Check if it's a regular file
        if (S_ISREG(file_stat.st_mode)) {
            if (file_stat.st_size > max_size) {
                max_size = file_stat.st_size;
                strncpy(largest_file, entry->d_name, sizeof(largest_file) - 1);
                largest_file[sizeof(largest_file) - 1] = '\0';
            }
        }
    }

    closedir(dir);

    if (max_size > 0) {
        printf("Largest file: %s\n", largest_file);
        printf("Size: %lld bytes\n", (long long)max_size);
    } else {
        printf("No regular files found in the directory.\n");
    }

    return 0;
}
/*****************************************************************************************************************/
41.Implement a C program to check if a file named "data.txt" is readable?
\// check_readable.c
#include <stdio.h>
#include <unistd.h>  // for access()

int main() {
    const char *filename = "data.txt";

    // Check read permission
    if (access(filename, R_OK) == 0) {
        printf("File '%s' is readable.\n", filename);
    } else {
        perror("File is not readable or does not exist");
    }

    return 0;
}
/**********************************************************************************************************/
42.Write a C program to create a new directory named "Logs" and move all files with the
".log" extension into it?
// move_logs.c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>
#include <errno.h>
#include <limits.h>

int has_log_extension(const char *filename) {
    const char *dot = strrchr(filename, '.');
    return dot && strcmp(dot, ".log") == 0;
}

int main() {
    const char *log_dir = "Logs";

    // Create Logs directory if it doesn't exist
    if (mkdir(log_dir, 0755) == -1 && errno != EEXIST) {
        perror("Failed to create Logs directory");
        return 1;
    }

    DIR *dir = opendir(".");
    if (dir == NULL) {
        perror("Failed to open current directory");
        return 1;
    }

    struct dirent *entry;
    char oldpath[PATH_MAX];
    char newpath[PATH_MAX];

    while ((entry = readdir(dir)) != NULL) {
        // Skip directories and hidden files
        if (entry->d_type != DT_REG || entry->d_name[0] == '.')
            continue;

        // Check if file has .log extension
        if (has_log_extension(entry->d_name)) {
            snprintf(oldpath, sizeof(oldpath), "./%s", entry->d_name);
            snprintf(newpath, sizeof(newpath), "./%s/%s", log_dir, entry->d_name);

            if (rename(oldpath, newpath) == -1) {
                perror("Failed to move file");
            } else {
                printf("Moved: %s -> %s\n", oldpath, newpath);
            }
        }
    }

    closedir(dir);
    return 0;
}
/*************************************************************************************************************/
43. Develop a C program to check if a file named "config.ini" is writable?
// check_writable.c
#include <stdio.h>
#include <unistd.h>  // for access()

int main() {
    const char *filename = "config.ini";

    // Check write permission
    if (access(filename, W_OK) == 0) {
        printf("File '%s' is writable.\n", filename);
    } else {
        perror("File is not writable or does not exist");
    }

    return 0;
}

```

```C
44.Implement a C program to read the contents of a text file named "instructions.txt" and
execute the instructions as shell commands?
// execute_instructions.c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_LINE 1024

int main() {
    FILE *fp = fopen("instructions.txt", "r");
    if (fp == NULL) {
        perror("Failed to open instructions.txt");
        return 1;
    }

    char line[MAX_LINE];

    while (fgets(line, sizeof(line), fp)) {
        // Remove newline character at the end
        line[strcspn(line, "\n")] = '\0';

        if (strlen(line) == 0) continue;  // Skip empty lines

        printf("Executing: %s\n", line);
        int result = system(line);

        if (result == -1) {
            perror("Failed to execute command");
        }
    }

    fclose(fp);
    return 0;
}
/*****************************************************************************************************************/
45. Write a C program to get the number of hard links to a file named "file.txt"?
// hardlink_count.c
#include <stdio.h>
#include <sys/stat.h>
#include <stdlib.h>

int main() {
    const char *filename = "file.txt";
    struct stat fileStat;

    if (stat(filename, &fileStat) == -1) {
        perror("Failed to get file status");
        return 1;
    }

    printf("File: %s\n", filename);
    printf("Number of hard links: %ld\n", (long)fileStat.st_nlink);

    return 0;
}
/*********************************************************************************************************************/
46.Develop a C program to copy the contents of all text files in a directory into a single file
named "combined.txt"?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>

#define MAX_PATH 1024
#define BUFFER_SIZE 4096

int endsWithTxt(const char *filename) {
    const char *dot = strrchr(filename, '.');
    return (dot && strcmp(dot, ".txt") == 0);
}

int isCombinedFile(const char *filename) {
    return strcmp(filename, "combined.txt") == 0;
}

int main() {
    DIR *dir;
    struct dirent *entry;
    FILE *outfile, *infile;
    char buffer[BUFFER_SIZE];

    char *directory = "."; // Current directory
    outfile = fopen("combined.txt", "w");
    if (!outfile) {
        perror("Unable to create combined.txt");
        return 1;
    }

    dir = opendir(directory);
    if (!dir) {
        perror("Unable to open directory");
        fclose(outfile);
        return 1;
    }

    while ((entry = readdir(dir)) != NULL) {
        if (entry->d_type == DT_REG && endsWithTxt(entry->d_name) && !isCombinedFile(entry->d_name)) {
            infile = fopen(entry->d_name, "r");
            if (!infile) {
                perror(entry->d_name);
                continue;
            }

            fprintf(outfile, "\n---- %s ----\n", entry->d_name); // Optional header
            size_t bytes;
            while ((bytes = fread(buffer, 1, BUFFER_SIZE, infile)) > 0) {
                fwrite(buffer, 1, bytes, outfile);
            }

            fclose(infile);
        }
    }

    closedir(dir);
    fclose(outfile);

    printf("All text files combined into combined.txt\n");
    return 0;
}
/***********************************************************************************************************************/
47.Implement a C program to recursively calculate the total size of all files in a directory
and its subdirectories?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>
#include <errno.h>

#define MAX_PATH 1024

long long get_directory_size(const char *path) {
    struct dirent *entry;
    struct stat info;
    DIR *dir;
    char fullpath[MAX_PATH];
    long long total_size = 0;

    dir = opendir(path);
    if (dir == NULL) {
        perror(path);
        return 0;
    }

    while ((entry = readdir(dir)) != NULL) {
        // Skip "." and ".."
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;

        snprintf(fullpath, sizeof(fullpath), "%s/%s", path, entry->d_name);

        if (lstat(fullpath, &info) == -1) {
            perror(fullpath);
            continue;
        }

        if (S_ISDIR(info.st_mode)) {
            // It's a directory: recurse
            total_size += get_directory_size(fullpath);
        } else if (S_ISREG(info.st_mode)) {
            // It's a regular file: add its size
            total_size += info.st_size;
        }
    }

    closedir(dir);
    return total_size;
}

int main(int argc, char *argv[]) {
    const char *start_path = "."; // Default: current directory
    if (argc > 1) {
        start_path = argv[1];
    }

    long long total_size = get_directory_size(start_path);
    printf("Total size of all files in '%s': %lld bytes\n", start_path, total_size);

    return 0;
}
/*************************************************************************************************************************/
48. Write a C program to get the number of bytes in a file named "data.bin"?
#include <stdio.h>

int main() {
    FILE *file = fopen("data.bin", "rb");  // Open in binary read mode
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    // Seek to the end of the file
    fseek(file, 0, SEEK_END);

    // Get the current position (i.e., the size of the file)
    long size = ftell(file);
    if (size == -1L) {
        perror("Error getting file size");
        fclose(file);
        return 1;
    }

    printf("Size of data.bin: %ld bytes\n", size);
    fclose(file);
    return 0;
}
/**********************************************************************************************************************/
49. Develop a C program to create a new directory named with the current timestamp in the
format "YYYY-MM-DD-HH-MM-SS"?
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <sys/stat.h>
#include <sys/types.h>

int main() {
    time_t now;
    struct tm *tm_info;
    char dirname[100];

    // Get current time
    time(&now);
    tm_info = localtime(&now);

    // Format: YYYY-MM-DD-HH-MM-SS
    strftime(dirname, sizeof(dirname), "%Y-%m-%d-%H-%M-%S", tm_info);

    // Create directory with 0755 permissions (rwxr-xr-x)
    if (mkdir(dirname, 0755) == 0) {
        printf("Directory '%s' created successfully.\n", dirname);
    } else {
        perror("Failed to create directory");
        return 1;
    }

    return 0;
}
/***********************************************************************************************************************/
50.Write a C program to create a new directory named "Documents" in the current
directory?
#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>

int main() {
    const char *dirname = "Documents";

    // Create directory with permission: rwxr-xr-x (0755)
    if (mkdir(dirname, 0755) == 0) {
        printf("Directory '%s' created successfully.\n", dirname);
    } else {
        perror("Failed to create directory");
        return 1;
    }

    return 0;
}
/****************************************************************************************************************/
51. Develop a C program to check if a file named "file.txt" exists in the current directory?
#include<stdio.h>
int main() {
    const char *filename = "file.txt";
    FILE *file = fopen(filename, "r");

    if (file) {
        printf("File '%s' exists in the current directory.\n", filename);
        fclose(file);
    } else {
        printf("File '%s' does NOT exist in the current directory.\n", filename);
    }

    return 0;
}
/*************************************************************************************************************/
52. Implement a C program to open a file named "data.txt" in read mode and display its
contents?
#include <stdio.h>
#include <stdlib.h>

int main() {
    const char *filename = "data.txt";
    FILE *file = fopen(filename, "r");

    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    char line[1024];  // Buffer to store each line

    printf("Contents of '%s':\n", filename);
    while (fgets(line, sizeof(line), file)) {
        printf("%s", line);  // Print line as-is
    }

    fclose(file);
    return 0;
}
/*****************************************************************************************************************************/
53. Write a C program to create a new text file named "output.txt" and write "Hello, World!"
to it?
#include <stdio.h>

int main() {
    const char *filename = "output.txt";
    FILE *file = fopen(filename, "w");  // Open file in write mode

    if (file == NULL) {
        perror("Error creating file");
        return 1;
    }

    fprintf(file, "Hello, World!\n");  // Write to the file
    fclose(file);

    printf("File '%s' created and message written successfully.\n", filename);
    return 0;
}
/*******************************************************************************************************************************/
54. Develop a C program to delete a file named "delete_me.txt" from the current directory?
#include <stdio.h>

int main() {
    // File name to delete
    const char *filename = "delete_me.txt";

    // Try deleting the file
    if (remove(filename) == 0) {
        printf("File '%s' deleted successfully.\n", filename);
    } else {
        perror("Error deleting the file");
    }

    return 0;
}
/*********************************************************************************************************/
55. Implement a C program to rename a file from "old_name.txt" to "new_name.txt"?
#include <stdio.h>

int main() {
    // File names
    const char *oldName = "old_name.txt";
    const char *newName = "new_name.txt";

    // Attempt to rename the file
    if (rename(oldName, newName) == 0) {
        printf("File renamed successfully from '%s' to '%s'.\n", oldName, newName);
    } else {
        perror("Error renaming the file");
    }

    return 0;
}
/********************************************************************************************************************************/
56. Write a C program to copy the contents of one file to another file?
#include <stdio.h>

int main() {
    FILE *sourceFile, *destFile;
    char ch;

    sourceFile = fopen("source.txt", "r");
    destFile = fopen("destination.txt", "w");

    if (sourceFile == NULL || destFile == NULL) {
        printf("Error opening files.\n");
        return 1;
    }

    // Copying character by character
    while ((ch = fgetc(sourceFile)) != EOF) {
        fputc(ch, destFile);
    }

    printf("File copied successfully.\n");

    fclose(sourceFile);
    fclose(destFile);

    return 0;
}
/**************************************************************************************************************************/
57. Develop a C program to move a file named "file.txt" to a directory named "Backup"?
#include <stdio.h>

int main() {
    const char *source = "file.txt";
    const char *destination = "Backup/file.txt";

    // Try to move (rename) the file
    if (rename(source, destination) == 0) {
        printf("File moved successfully to Backup folder.\n");
    } else {
        perror("Error moving file");
    }

    return 0;
}
/**********************************************************************************************************************/
58. Implement a C program to list all files and directories in the current directory?
#include <stdio.h>
#include <dirent.h>

int main() {
    struct dirent *entry;
    DIR *directory = opendir(".");

    if (directory == NULL) {
        perror("Unable to open current directory");
        return 1;
    }

    printf("Contents of current directory:\n");
    while ((entry = readdir(directory)) != NULL) {
        printf("%s\n", entry->d_name);
    }

    closedir(directory);
    return 0;
}
/*****************************************************************************************************************/
59. Write a C program to get the size of a file named "data.txt"?
#include <stdio.h>

int main() {
    FILE *file = fopen("data.txt", "rb");  // Open in binary mode

    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    fseek(file, 0, SEEK_END);        // Move pointer to the end
    long size = ftell(file);         // Get current pointer position (file size)
    fclose(file);                    // Close the file

    if (size == -1L) {
        perror("Error getting file size");
        return 1;
    }

    printf("Size of 'data.txt': %ld bytes\n", size);
    return 0;
}
/*************************************************************************************************************/
60. Develop a C program to create a new directory named "Pictures" in the parent
directory?
#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <errno.h>

int main() {
    const char *dir_path = "../Pictures";  // Parent directory

    if (mkdir(dir_path, 0777) == 0) {
        printf("Directory 'Pictures' created in parent directory.\n");
    } else {
        perror("Error creating directory");
    }

    return 0;
}
/**************************************************************************************************************/
61. Develop a C program to count the number of lines in a file named "log.txt"?
#include <stdio.h>
int main() {
    FILE *file = fopen("log.txt", "r");
    int lines = 0;
    char ch;

    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    // Read character by character and count newlines
    while ((ch = fgetc(file)) != EOF) {
        if (ch == '\n') {
            lines++;
        }
    }

    fclose(file);

    printf("Number of lines in 'log.txt': %d\n", lines);
    return 0;
}
/************************************************************************************************************/
62. Implement a C program to append "Goodbye!" to the end of an existing file named
"message.txt"?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        FILE *file=fopen("message.txt","a");
        if(file==NULL)
        {
                perror("error opening file");
                return 1;
        }
        fprintf(file,"goodbye\n");
        fclose(file);
        printf("\"goodbye!\" has been appended to message.txt\n");
        return 0;
}
63. Write a C program to create a symbolic link named "link.txt" to a file named
"target.txt"?
#include<stdio.h>
#include<unistd.h>
int main()
{
        const char *target="target.txt";
        const char *linkname="link.txt";
        if(symlink(target,linkname)==0)
        {
                printf("symbolic link 'link.txt' created pointing target.txt\n");
        }
        else
        {
                perror("error creating symbolic link");
                return 1;
        }
        return 0;
}
/*******************************************************************************************************************/
64. Develop a C program to change the permissions of a file named "file.txt" to read-only?
#include <windows.h> is a preprocessor directive in C or C++ that tells the compiler to include the Windows API header file, which provides access to thousands of functions, macros, and data types specific to the Windows operating system.
🔍 What Does <windows.h> Provide?

It gives you access to:
Feature	Description
File handling	CreateFile(), SetFileAttributes(), DeleteFile()
Window management	CreateWindow(), ShowWindow(), MessageBox()
Process and thread control	CreateProcess(), CreateThread()
Memory management	VirtualAlloc(), GlobalAlloc()
System information	GetSystemTime(), GetComputerName()
Graphics and drawing	GDI functions like BitBlt(), DrawText()
Registry access	RegOpenKey(), RegQueryValue()
🧠 Example: Set a File to Read-Only on Windows

#include <windows.h>
#include <stdio.h>

int main() {
    const char *filename = "file.txt";

    if (SetFileAttributesA(filename, FILE_ATTRIBUTE_READONLY)) {
        printf("Set 'file.txt' as read-only.\n");
    } else {
        printf("Failed to change file attributes. Error code: %lu\n", GetLastError());
    }

    return 0;
}

⚠️ Important Notes

    <windows.h> is only available on Windows platforms.

    It includes many subheaders internally (like winuser.h, winbase.h, etc.), so it can slow down compilation if not managed carefull
/***************************************************************************************************************************************/
65. Implement a C program to change the ownership of a file named "file.txt" to the user
"user1?
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pwd.h>
#include <sys/types.h>

int main() {
    const char *filename = "file.txt";
    const char *username = "user1";

    // Get user information
    struct passwd *pwd = getpwnam(username);
    if (pwd == NULL) {
        perror("User not found");
        return 1;
    }

    // Change ownership: user1 as owner, leave group unchanged (-1)
    if (chown(filename, pwd->pw_uid, -1) == 0) {
        printf("Ownership of '%s' changed to user '%s'\n", filename, username);
    } else {
        perror("Error changing file ownership");
        return 1;
    }

    return 0;
}
/****************************************************************************************************************************/
66. Write a C program to get the last modified timestamp of a file named "file.txt"?
#include<stdio.h>
#include<sys/stat.h>
#include<time.h>
int main()
{
        struct stat filestat;
        if(stat("file.txt",&filestat)==-1)
        {
                perror("error receiving file info");
                return 1;
        }
        printf("last modified time of 'file.txt':%s",ctime(&filestat.st_mtime));
        return 0;
}
/************************************************************************************************************************/
67. Develop a C program to create a temporary file and write some data to it?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        FILE *tempfile=tmpfile();
        if(tempfile==NULL)
        {
                perror("error creating temporary file");
                return 1;
        }
        fprintf(tempfile,"this is temporary data.\n");
        rewind(tempfile);
        char buffer[100];
        while(fgets(buffer,sizeof(buffer),tempfile))
        {
                printf("%s",buffer);
        }
        fclose(tempfile);
        return 0;
}
/**********************************************************************************************************************/
68. Implement a C program to get the size of a file named "image.jpg"?
#include <stdio.h>

int main() {
    FILE *file = fopen("image.jpg", "rb");  // Open in binary mode
    long size;

    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    fseek(file, 0, SEEK_END);   // Move to end of file
    size = ftell(file);         // Get current position (file size)
    fclose(file);

    if (size == -1L) {
        perror("Error getting file size");
        return 1;
    }

    printf("Size of 'image.jpg': %ld bytes\n", size);
    return 0;
}
/***************************************************************************************************************************/
69. Write a C program to create a new text file named "notes.txt" and write multiple lines of
text to it?
#include <stdio.h>

int main() {
    FILE *file = fopen("notes.txt", "w");  // "w" = write mode (creates or overwrites)

    if (file == NULL) {
        perror("Error creating file");
        return 1;
    }

    // Write multiple lines to the file
    fprintf(file, "This is the first line.\n");
    fprintf(file, "This is the second line.\n");
    fprintf(file, "This is the third line.\n");

    fclose(file);

    printf("Multiple lines written to 'notes.txt'\n");
    return 0;
}
/************************************************************************************************************************/
70. Develop a C program to count the number of words in a file named "essay.txt"?
#include <stdio.h>
#include <ctype.h>

int main() {
    FILE *file = fopen("essay.txt", "r");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    int ch, inWord = 0, wordCount = 0;

    while ((ch = fgetc(file)) != EOF) {
        if (isspace(ch)) {
            if (inWord) {
                wordCount++;
                inWord = 0;
            }
        } else {
            inWord = 1;
        }
    }

    // If the last word doesn't end with space or newline
    if (inWord) {
        wordCount++;
    }

    fclose(file);

    printf("Total words in 'essay.txt': %d\n", wordCount);
    return 0;
}
/***********************************************************************************************************************/
71. Write a C program to create a symbolic link named "shortcut.txt" to a file named
"target.txt"?
#include <stdio.h>
#include <unistd.h>

int main() {
    const char *target = "target.txt";
    const char *link = "shortcut.txt";

    // Create symbolic link
    if (symlink(target, link) == 0) {
        printf("Symbolic link '%s' created pointing to '%s'\n", link, target);
    } else {
        perror("symlink");
    }

    return 0;
}
/*********************************************************************************************************************/
72. Develop a C program to change the permissions of a file named "important.doc" to read
and write for the owner only?
#include<stdio.h>
#include<stdlib.h>
#include<sys/stat.h>
int main()
{
        const char *filename="important.doc";
        if(chmod(filename,S_IRUSR|S_IWUSR)==-1)
        {
                perror("chmod failed");
                return EXIT_FAILURE;
        }
        printf("permissioms of '%s' changed to read and write for owner only(0600).\n",filename);
        return EXIT_SUCCESS;
}
/**********************************************************************************************************************/
73. Write a C program to get the last access time of a file named "data.txt"?
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <time.h>

int main() {
    const char *filename = "data.txt";
    struct stat file_stat;

    // Get file statistics
    if (stat(filename, &file_stat) == -1) {
        perror("stat failed");
        return EXIT_FAILURE;
    }

    // Convert last access time to readable format
    printf("Last access time of '%s': %s", filename, ctime(&file_stat.st_atime));

    return EXIT_SUCCESS;
}
/*************************************************************************************************************************/
74. Develop a C program to read and display the contents of a CSV file named "data.csv"?
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *file;
    char buffer[1024];
    const char *filename = "data.csv";

    // Open the CSV file for reading
    file = fopen(filename, "r");
    if (file == NULL) {
        perror("Error opening file");
        return EXIT_FAILURE;
    }

    printf("Contents of '%s':\n", filename);
    
    // Read and print each line
    while (fgets(buffer, sizeof(buffer), file)) {
        printf("%s", buffer);  // buffer already includes newline if present
    }

    fclose(file);
    return EXIT_SUCCESS;
}
/****************************************************************************************************************************/
75. Implement a C program to truncate a file named "file.txt" to a specified
length?
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>

int main() {
    const char *filename = "file2.txt";
    off_t new_length;

    // Ask user for the desired length
    printf("Enter the length to truncate '%s' to: ", filename);
    if (scanf("%ld", &new_length) != 1 || new_length < 0) {
        fprintf(stderr, "Invalid input.\n");
        return EXIT_FAILURE;
    }

    // Truncate the file to the given length
    if (truncate(filename, new_length) == -1) {
        perror("truncate failed");
        return EXIT_FAILURE;
    }

    printf("File '%s' truncated to %ld bytes.\n", filename, new_length);
    return EXIT_SUCCESS;
}
/****************************************************************************************************************************/
76. Write a C program to search for a specific word in a file named "data.txt" and display
the line number(s) where it occurs?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

#define MAX_LINE_LENGTH 1024

int containsWord(const char *line, const char *word) {
    const char *p = line;
    size_t word_len = strlen(word);

    while ((p = strstr(p, word)) != NULL) {
        // Check word boundaries
        if ((p == line || !isalnum(*(p - 1))) &&
            (!isalnum(*(p + word_len)))) {
            return 1;
        }
        p += word_len;
    }

    return 0;
}

int main() {
    FILE *file;
    char line[MAX_LINE_LENGTH];
    char word[100];
    int lineNumber = 0;
    int found = 0;

    printf("Enter the word to search: ");
    scanf("%s", word);

    file = fopen("data.txt", "r");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    while (fgets(line, MAX_LINE_LENGTH, file)) {
        lineNumber++;
        if (containsWord(line, word)) {
            printf("Word found on line %d\n", lineNumber);
            found = 1;
        }
    }

    if (!found) {
        printf("Word not found in the file.\n");
    }

    fclose(file);
    return 0;
}
/********************************************************************************************************************************/
77. Develop a C program to get the file type (regular file, directory, symbolic link, etc.) of a
given path?
#include <stdio.h>
#include <sys/stat.h>
#include <unistd.h>

void print_file_type(const char *path) {
    struct stat fileStat;

    // Use lstat to avoid following symbolic links
    if (lstat(path, &fileStat) == -1) {
        perror("Error getting file status");
        return;
    }

    printf("File type of '%s': ", path);

    if (S_ISREG(fileStat.st_mode))
        printf("Regular file\n");
    else if (S_ISDIR(fileStat.st_mode))
        printf("Directory\n");
    else if (S_ISLNK(fileStat.st_mode))
        printf("Symbolic link\n");
    else if (S_ISCHR(fileStat.st_mode))
        printf("Character device\n");
    else if (S_ISBLK(fileStat.st_mode))
        printf("Block device\n");
    else if (S_ISFIFO(fileStat.st_mode))
        printf("FIFO/Named pipe\n");
    else if (S_ISSOCK(fileStat.st_mode))
        printf("Socket\n");
    else
        printf("Unknown type\n");
}

int main() {
    char path[512];

    printf("Enter the path: ");
    scanf("%s", path);

    print_file_type(path);

    return 0;
}
/*******************************************************************************************************************/
78. Implement a C program to read and display the contents of a binary file named
"binary.bin"?
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *file;
    unsigned char buffer[1024];
    size_t bytesRead;
    int i;

    // Open the binary file in read mode
    file = fopen("binary.bin", "rb");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    printf("Contents of binary.bin (in hexadecimal):\n");

    // Read and display file content in hex format
    while ((bytesRead = fread(buffer, 1, sizeof(buffer), file)) > 0) {
        for (i = 0; i < bytesRead; i++) {
            printf("%02X ", buffer[i]);
            if ((i + 1) % 16 == 0)  // Print 16 bytes per line
                printf("\n");
        }
    }

    printf("\n");

    fclose(file);
    return 0;
}
/*************************************************************************************************************************/
79. Implement a C program to create a new directory named "Logs" and move all files with
the ".log" extension into it?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>

int has_log_extension(const char *filename) {
    const char *ext = strrchr(filename, '.');
    return (ext && strcmp(ext, ".log") == 0);
}

int main() {
    DIR *dir;
    struct dirent *entry;
    struct stat st;

    // Create "Logs" directory if it doesn't exist
    if (stat("Logs", &st) == -1) {
        if (mkdir("Logs", 0755) != 0) {
            perror("Failed to create Logs directory");
            return 1;
        }
    }

    // Open current directory
    dir = opendir(".");
    if (dir == NULL) {
        perror("Failed to open current directory");
        return 1;
    }

    // Process files
    while ((entry = readdir(dir)) != NULL) {
        // Skip directories
        if (entry->d_type == DT_REG && has_log_extension(entry->d_name)) {
            char new_path[512];
            snprintf(new_path, sizeof(new_path), "Logs/%s", entry->d_name);

            if (rename(entry->d_name, new_path) != 0) {
                perror("Failed to move file");
            } else {
                printf("Moved: %s -> %s\n", entry->d_name, new_path);
            }
        }
    }

    closedir(dir);
    return 0;
}
/**************************************************************************************************************************/
80. Write a C program to check if a file named "config.ini" is writable?
#include <stdio.h>
#include <unistd.h>

int main() {
    const char *filename = "config.ini";

    // Check if the file exists and is writable
    if (access(filename, F_OK) != 0) {
        printf("File '%s' does not exist.\n", filename);
    } else if (access(filename, W_OK) == 0) {
        printf("File '%s' is writable.\n", filename);
    } else {
        printf("File '%s' is not writable.\n", filename);
    }

    return 0;
}
/******************************************************************************************************************************/
81. Develop a C program to read the contents of a text file named "instructions.txt" and
execute the instructions as shell commands?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_LINE 1024

int main() {
    FILE *file;
    char line[MAX_LINE];

    file = fopen("instructions.txt", "r");
    if (file == NULL) {
        perror("Error opening instructions.txt");
        return 1;
    }

    while (fgets(line, sizeof(line), file)) {
        // Remove newline character at end
        line[strcspn(line, "\n")] = 0;

        if (strlen(line) == 0)
            continue; // skip empty lines

        printf("Executing: %s\n", line);
        int result = system(line);

        if (result == -1) {
            perror("Error executing command");
        }
    }

    fclose(file);
    return 0;
    }
/******************************************************************************************************************************/
82. Develop a C program to read data from a binary file named "data.bin" and display it in
hexadecimal format?
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *file;
    unsigned char buffer[16];  // Buffer to read 16 bytes at a time
    size_t bytesRead;
    int offset = 0;

    file = fopen("data.bin", "rb");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }

    printf("Hexadecimal contents of data.bin:\n\n");

    while ((bytesRead = fread(buffer, 1, sizeof(buffer), file)) > 0) {
        // Print offset
        printf("%08X  ", offset);

        // Print hex values
        for (size_t i = 0; i < bytesRead; i++) {
            printf("%02X ", buffer[i]);
        }

        // Fill in spaces if line is short
        for (size_t i = bytesRead; i < 16; i++) {
            printf("   ");
        }

        // Print ASCII representation
        printf(" |");
        for (size_t i = 0; i < bytesRead; i++) {
            if (buffer[i] >= 32 && buffer[i] <= 126) {
                printf("%c", buffer[i]);
            } else {
                printf(".");
            }
        }
        printf("|\n");

        offset += bytesRead;
    }

    fclose(file);
    return 0;
}
/*****************************************************************************************************************/
83. Develop a C program to recursively copy all files and directories from one directory to
another?
repeated question
/***************************************************************************************************************/
84. Develop a C program to get the file type (regular file, directory, symbolic link, etc.) of a
given path?
#include <stdio.h>
#include <sys/stat.h>
#include <unistd.h>

void get_file_type(const char *path) {
    struct stat fileStat;

    // Use lstat to avoid following symlinks
    if (lstat(path, &fileStat) == -1) {
        perror("Error retrieving file status");
        return;
    }

    printf("File type of '%s': ", path);

    if (S_ISREG(fileStat.st_mode))
        printf("Regular file\n");
    else if (S_ISDIR(fileStat.st_mode))
        printf("Directory\n");
    else if (S_ISLNK(fileStat.st_mode))
        printf("Symbolic link\n");
    else if (S_ISCHR(fileStat.st_mode))
        printf("Character device\n");
    else if (S_ISBLK(fileStat.st_mode))
        printf("Block device\n");
    else if (S_ISFIFO(fileStat.st_mode))
        printf("FIFO (named pipe)\n");
    else if (S_ISSOCK(fileStat.st_mode))
        printf("Socket\n");
    else
        printf("Unknown\n");
}

int main() {
    char path[512];

    printf("Enter the file path: ");
    scanf("%s", path);

    get_file_type(path);

    return 0;
}
/*********************************************************************************************************************/

```







