## 基本I/O

This lesson covers the Java platform classes used for basic I/O. It first focuses on *I/O Streams*, a powerful concept that greatly simplifies I/O operations. The lesson also looks at serialization, which lets a program write whole objects out to streams and read them back again. Then the lesson looks at file I/O and file system operations, including random access files.

Most of the classes covered in the `I/O Streams` section are in the `java.io` package. Most of the classes covered in the `File I/O` section are in the `java.nio.file` package.

## [I/O Streams](https://docs.oracle.com/javase/tutorial/essential/io/streams.html)

- [Byte Streams](https://docs.oracle.com/javase/tutorial/essential/io/bytestreams.html) handle I/O of raw binary data.
- [Character Streams](https://docs.oracle.com/javase/tutorial/essential/io/charstreams.html) handle I/O of character data, automatically handling translation to and from the local character set.
- [Buffered Streams](https://docs.oracle.com/javase/tutorial/essential/io/buffers.html) optimize input and output by reducing the number of calls to the native API.
- [Scanning and Formatting](https://docs.oracle.com/javase/tutorial/essential/io/scanfor.html) allows a program to read and write formatted text.
- [I/O from the Command Line](https://docs.oracle.com/javase/tutorial/essential/io/cl.html) describes the Standard Streams and the Console object.
- [Data Streams](https://docs.oracle.com/javase/tutorial/essential/io/datastreams.html) handle binary I/O of primitive data type and `String` values.
- [Object Streams](https://docs.oracle.com/javase/tutorial/essential/io/objectstreams.html) handle binary I/O of objects.

## [File I/O (Featuring NIO.2)](https://docs.oracle.com/javase/tutorial/essential/io/fileio.html)

- [What is a Path?](https://docs.oracle.com/javase/tutorial/essential/io/path.html) examines the concept of a path on a file system.
- [The Path Class](https://docs.oracle.com/javase/tutorial/essential/io/pathClass.html) introduces the cornerstone class of the `java.nio.file` package.
- [Path Operations](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html) looks at methods in the `Path` class that deal with syntactic operations.
- [File Operations](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html) introduces concepts common to many of the file I/O methods.
- [Checking a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/check.html) shows how to check a file's existence and its level of accessibility.
- [Deleting a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/delete.html).
- [Copying a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/copy.html).
- [Moving a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/move.html).
- [Managing Metadata](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) explains how to read and set file attributes.
- [Reading, Writing and Creating Files](https://docs.oracle.com/javase/tutorial/essential/io/file.html) shows the stream and channel methods for reading and writing files.
- [Random Access Files](https://docs.oracle.com/javase/tutorial/essential/io/rafs.html) shows how to read or write files in a non-sequentially manner.
- [Creating and Reading Directories](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html) covers API specific to directories, such as how to list a directory's contents.
- [Links, Symbolic or Otherwise](https://docs.oracle.com/javase/tutorial/essential/io/links.html) covers issues specific to symbolic and hard links.
- [Walking the File Tree](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) demonstrates how to recursively visit each file and directory in a file tree.
- [Finding Files](https://docs.oracle.com/javase/tutorial/essential/io/find.html) shows how to search for files using pattern matching.
- [Watching a Directory for Changes](https://docs.oracle.com/javase/tutorial/essential/io/notification.html) shows how to use the watch service to detect files that are added, removed or updated in one or more directories.
- [Other Useful Methods](https://docs.oracle.com/javase/tutorial/essential/io/misc.html) covers important API that didn't fit elsewhere in the lesson.
- [Legacy File I/O Code](https://docs.oracle.com/javase/tutorial/essential/io/legacy.html) shows how to leverage `Path` functionality if you have older code using the `java.io.File`class. A table mapping `java.io.File` API to `java.nio.file` API is provided.

## The I/O Classes in Action

Many of the examples in the next trail, [Custom Networking](https://docs.oracle.com/javase/tutorial/networking/index.html) use the I/O streams described in this lesson to read from and write to network connections.

------

**Security consideration:** Some I/O operations are subject to approval by the current security manager. The example programs contained in these lessons are standalone applications, which by default have no security manager. To work in an applet, most of these examples would have to be modified. See [What Applets Can and Cannot Do](https://docs.oracle.com/javase/tutorial/deployment/applet/security.html) for information about the security restrictions placed on applets.

------

