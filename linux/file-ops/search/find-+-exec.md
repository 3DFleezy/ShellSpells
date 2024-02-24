# Find + Exec

Change html files to mode 644:

```bash
find /usr/local -name "*.html"-type f -exec chmod 644 {} \;
```

Change cgi files to mode 755:

```bash
find htdocs cgi-bin -name "*.cgi"-type f -exec chmod 755 {} \;
```

Run ls command on files found:

```bash
find .-name "*.pl"-exec ls -ld {} \;
```

Find and tar:

```bash
find .-type f -name "*.java"|xargs tar cvf myfile.tar
```

```bash
find .-type f -name "*.java"|xargs tar rvf myfile.tar
```

Find and Delete:

```bash
find .-type f -name "Foo*"-exec rm {} \;
```

```bash
find .-type d -name CVS -exec rm -r {} \;
```

Find and Copy:

```bash
find .-type f -name "*.mp3"-exec cp {} /tmp/MusicFiles \;
```
