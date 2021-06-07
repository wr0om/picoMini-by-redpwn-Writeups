## Details
- Category: Web Exploitation
- Points: 100

## Description
```
My dog-sitter's brother made this website but I can't get in; can you help?
```
and the site [login.mars.picoctf.net](login.mars.picoctf.net)
## Hint
```
(None)
```
## Solution
We are met with a basic login page:

![image](https://user-images.githubusercontent.com/59180254/121037089-d9af0280-c7b7-11eb-9dfa-973119953639.png)

There's nothing special about the HTML of the page, so I went to the index.js file listed on the HTML.
Here's the code:
```javascript
(async()=>{
    await new Promise((e=>window.addEventListener("load", e))),
    document.querySelector("form").addEventListener("submit", (e=>{
        e.preventDefault();
        const r = {
            u: "input[name=username]",
            p: "input[name=password]"
        }
          , t = {};
        for (const e in r)
            t[e] = btoa(document.querySelector(r[e]).value).replace(/=/g, "");
        return "YWRtaW4" !== t.u ? alert("Incorrect Username") : "cGljb0NURns1M3J2M3JfNTNydjNyXzUzcnYzcl81M3J2M3JfNTNydjNyfQ" !== t.p ? alert("Incorrect Password") : void alert(`Correct Password! Your flag is ${atob(t.p)}.`)
    }
    ))
}
)();
```

We can see that the values we give the site (username and password) are being transferred to the **btoa** action, and then compared to "random" strings.

This boolean expression checks the login information:
```javascript
"YWRtaW4" !== t.u ? alert("Incorrect Username") : "cGljb0NURns1M3J2M3JfNTNydjNyXzUzcnYzcl81M3J2M3JfNTNydjNyfQ" !== t.p ? alert("Incorrect Password") : void alert(`Correct Password! Your flag is ${atob(t.p)}.`)
```

The btoa function encodes values with base64, so let's turn them back (you can do it with a decoder online):
* YWRtaW4 = admin
* cGljb0NURns1M3J2M3JfNTNydjNyXzUzcnYzcl81M3J2M3JfNTNydjNyfQ = picoCTF{53rv3r_53rv3r_53rv3r_53rv3r_53rv3r}

That's it, this is the flag - picoCTF{53rv3r_53rv3r_53rv3r_53rv3r_53rv3r}
