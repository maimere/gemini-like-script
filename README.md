> [!CAUTION]
> This is a ancient and amateur script I wrote way back when I was still developing my programming skills. Use at your own risk.

### A CGI script that allows users to (un)like pages on the Gemini protocol.

### This was used and published on my former gemini server. Here I keep the original code and explanation I wrote at the time.

## Explanation

The script saves the IP of the user after he/she likes the page. Only the IPv4 is saved, not even the date, hour or other information. The IP is written on a file linked to that page. Anytime later, if the user is connected through the same IP, it is possible for him/her to unlike the page, having the IP erased from that file. There is no record of every likes that have ever been registered. If you like a page, and immediately unlike it, I will never know.

## Files

### Private files (not made public directly at you Gemini capsule directory)

- `likescript`: Prints the number of likes and the like/unlike button.
This file is embedded into the page, which has to be itself a CGI executable. Personally, I build my pages as shell scripts, so I would just have this line at the end of the page, and the content will show up: `/dir-to-file/likescript`

- `likeable`: Each line of this file is part of the URL as set by the `SCRIPT_NAME` variable when checked by the `likescript` file, and the `PATH_INFO` variable when checked by the `like` file.
Example taken directly from my capsule:
```
$ cat likeable
/capsule/20201201-liftoff.log
/capsule/20201227-like-a-laika.log
/capsule/20201229-my-programming-skills.log
```

 - other files: These files are named after the files in the `likeable` file, but their content is only the IP of those users who liked the page with the same name.

### Public file (which can be summoned directly by the client)

- `like`: Registers the like or unline of the page which part of URL is appended. For example: When summoned as `gemini://domain.com/like/20210101-hello.gmi`, the `gemini://domain.com/20210101-hello.gmi` page gets a like or unlike, but only if `/20210101-hello.gmi` is a line of the `likeable` file.
