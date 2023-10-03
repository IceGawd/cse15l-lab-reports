# cd
## no arguments

```
[user@sahara ~]$ cd
[user@sahara ~]$ 
```
Nothing happened because we were already in the home directory. cd without arguments moves you into the home directory.

## directory argument

```
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$ 
```
It changed directory into the given directory. No error as it worked as intended.

## file argument

```
[user@sahara ~/lecture1]$ cd Hello.java 
bash: cd: Hello.java: Not a directory
[user@sahara ~/lecture1]$ 
```
It gave an error because cd expects directory arguments and a file was given.

# ls
## no arguments

```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
[user@sahara ~/lecture1]$ 
```
It listed all of the files and directories in the current working directory, as intended 

## directory argument

```
[user@sahara ~/lecture1]$ ls messages/
en-us.txt  es-mx.txt  in-hi.txt  zh-cn.txt
[user@sahara ~/lecture1]$ 
```
It listed all of the files and directories in the directory given as an argument.

## file argument

```
[user@sahara ~/lecture1]$ ls Hello.java 
Hello.java
[user@sahara ~/lecture1]$ 
```
Strangely enough, it just printed the name of the file given without error. My guess is that ls will print all of the files and directories given to it, or just print everything in the current working diretory if no arguments are given.

# cat
## no arguments

```
[user@sahara ~/lecture1]$ cat
^C
[user@sahara ~/lecture1]$ 
```
Running cat without any argument got stuck in an infinite loop (which I had to escape with Ctrl+C). This is an error because cat will print files given, and it cannot have a 'default' so an argument needs to be given.

## directory argument

```
[user@sahara ~/lecture1]$ cat messages/
cat: messages/: Is a directory
[user@sahara ~/lecture1]$ 
```
It gave an error as, once again, cat prints the contents of a file and it was not expecting to be given a directory.

## file argument

```
[user@sahara ~/lecture1]$ cat Hello.java 
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}[user@sahara ~/lecture1]$ 
```
Finally, with the proper argument of a file, cat works as intended. An interesting note is that there was no empty line at the end of `Hello.java` so after printing the final `}`, it just printed `[user@sahara ~/lecture1]$ ` immediately after with no new-line.
