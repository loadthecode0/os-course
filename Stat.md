The `stat()` function in Unix-like operating systems is used to retrieve detailed information about a file or a directory. This information includes file size, ownership, permissions, timestamps, and other metadata.

---

### **Function Prototype**

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>

int stat(const char *pathname, struct stat *statbuf);
```

### **Parameters**

1. **`pathname`**:
    
    - The path to the file or directory whose information is to be retrieved.
2. **`statbuf`**:
    
    - A pointer to a `struct stat` where the file or directory metadata will be stored.

### **Return Value**

- **0**: On success, the `statbuf` is filled with the file's metadata.
- **-1**: On failure, with `errno` set to indicate the error.

---

### **The `struct stat` Structure**

The `struct stat` is defined in `<sys/stat.h>` and contains various fields. Common fields include:

|Field|Description|
|---|---|
|`st_mode`|File type and mode (permissions).|
|`st_uid`|User ID of the owner.|
|`st_gid`|Group ID of the owner.|
|`st_size`|Size of the file in bytes.|
|`st_atime`|Time of last access.|
|`st_mtime`|Time of last modification.|
|`st_ctime`|Time of last status change.|
|`st_nlink`|Number of hard links.|
|`st_ino`|Inode number (unique identifier for the file).|
|`st_dev`|ID of the device containing the file.|
|`st_blocks`|Number of 512-byte blocks allocated.|

---

### **Usage Example**

#### Basic Example to Get File Information

```c
#include <stdio.h>
#include <sys/stat.h>
#include <unistd.h>

int main() {
    struct stat fileStat;

    // File path to check
    const char *filePath = "example.txt";

    // Call stat to get file info
    if (stat(filePath, &fileStat) < 0) {
        perror("stat failed");
        return 1;
    }

    // Print file information
    printf("File: %s\n", filePath);
    printf("Size: %ld bytes\n", fileStat.st_size);
    printf("Owner UID: %d\n", fileStat.st_uid);
    printf("Permissions: %o\n", fileStat.st_mode & 0777);
    printf("Last modified: %ld\n", fileStat.st_mtime);

    return 0;
}
```

---

### **Interpreting Permissions (`st_mode`)**

The `st_mode` field contains both the file type and permission bits.

#### To Check the File Type:

Use macros defined in `<sys/stat.h>`:

- **`S_ISREG(st_mode)`**: Regular file.
- **`S_ISDIR(st_mode)`**: Directory.
- **`S_ISCHR(st_mode)`**: Character device.
- **`S_ISBLK(st_mode)`**: Block device.
- **`S_ISFIFO(st_mode)`**: FIFO (named pipe).
- **`S_ISLNK(st_mode)`**: Symbolic link.
- **`S_ISSOCK(st_mode)`**: Socket.

#### To Extract Permissions:

The file permissions can be obtained using the bitmask `0777`:

- Example: `fileStat.st_mode & 0777`

---

### **Sample Output**

For a file named `example.txt`:

```
File: example.txt
Size: 1024 bytes
Owner UID: 1000
Permissions: 644
Last modified: 1680524234
```

---

### **Common Variants of `stat()`**

- **`lstat()`**:
    - Similar to `stat()` but does not follow symbolic links. Instead, it retrieves information about the link itself.
- **`fstat()`**:
    - Used to get file information for an open file descriptor.

---

### **Key Notes**

1. **Symbolic Links**:
    
    - `stat()` follows symbolic links and retrieves information about the target file.
    - Use `lstat()` if you need information about the link itself.
2. **File Type**:
    
    - The file type can be checked using macros like `S_ISREG` or `S_ISDIR`.
3. **Permissions**:
    
    - Combine `st_mode` with `S_IRUSR`, `S_IWUSR`, and other bitwise masks to analyze permission settings.
4. **Error Handling**:
    
    - Always check the return value of `stat()` to handle errors gracefully (e.g., missing file or insufficient permissions).

---

The `stat()` function is a powerful tool for retrieving detailed information about files and directories, and it is widely used in system programming and file management utilities.