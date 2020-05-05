# codeSnippetsFromInternet

### ShallowCopy VS DeepCopy [src]((https://stackoverflow.com/a/184754))
```C++
char * Source = "Hello, world.";

char * ShallowCopy = Source;    

char * DeepCopy = new char(strlen(Source)+1);
strcpy(DeepCopy,Source);        
```
'ShallowCopy' points to the same location in memory as 'Source' does. 'DeepCopy' points to a different location in memory, but the contents are the same.

### CommandLine Progress bar CPP [src](https://stackoverflow.com/a/36315819)
```C++
#define PBSTR "||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||"
#define PBWIDTH 60

void printProgress (double percentage)
{
    int val = (int) (percentage * 100);
    int lpad = (int) (percentage * PBWIDTH);
    int rpad = PBWIDTH - lpad;
    printf ("\r%3d%% [%.*s%*s]", val, lpad, PBSTR, rpad, "");
    fflush (stdout);
}
```

### Safe Getline [src](https://stackoverflow.com/a/6089413)

```CPP
std::istream& safeGetline(std::istream& is, std::string& t)
{
    t.clear();

    // The characters in the stream are read one-by-one using a std::streambuf.
    // That is faster than reading them one-by-one using the std::istream.
    // Code that uses streambuf this way must be guarded by a sentry object.
    // The sentry object performs various tasks,
    // such as thread synchronization and updating the stream state.

    std::istream::sentry se(is, true);
    std::streambuf* sb = is.rdbuf();

    for(;;) {
        int c = sb->sbumpc();
        switch (c) {
        case '\n':
            return is;
        case '\r':
            if(sb->sgetc() == '\n')
                sb->sbumpc();
            return is;
        case std::streambuf::traits_type::eof():
            // Also handle the case when the last line has no line ending
            if(t.empty())
                is.setstate(std::ios::eofbit);
            return is;
        default:
            t += (char)c;
        }
    }
}
```
### print 256 colour palette

curl -s https://gist.githubusercontent.com/HaleTom/89ffe32783f89f403bba96bd7bcd1263/raw/ | bash

![alt text][image]

[image]: https://i.imgur.com/okBgrw4.png 
