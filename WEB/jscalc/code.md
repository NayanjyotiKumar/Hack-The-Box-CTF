# [jscalc](https://app.hackthebox.com/challenges/jscalc)
Author: Nayanjyoti Kumar


# Table of Contents

1. BagBounty
2. Attack Vector
3. Payload


## BagBounty

In a first phase we go `bagbouty`, we were provided with the code is a good way to start.

    .
    ├── build-docker.sh
    ├── challenge
    │   ├── helpers
    │   │   └── calculatorHelper.js
    │   ├── index.js
    │   ├── package.json
    │   ├── package-lock.json
    │   ├── routes
    │   │   └── index.js
    │   ├── static
    │   │   ├── css
    │   │   │   └── main.css
    │   │   ├── favicon.png
    │   │   └── js
    │   │       └── main.js
    │   ├── views
    │   │   └── index.html
    │   └── yarn.lock
    ├── config
    │   └── supervisord.conf
    ├── Dockerfile
    ├── flag.txt
    └── supervisord.conf

Immediately in the file `web_jscalc/challenge/helpers/calculatorHelper.js` we find the presence of an `eval()` function.

    module.exports = {
        calculate(formula) {
            try {
                return eval(`(function() { return ${ formula } ;}())`);
    
            } catch (e) {
                if (e instanceof SyntaxError) {
                    return 'Something went wrong!';
                }
            }
        }
    }

<span class="underline">Attenction!</span>

    return eval(`(function() { return ${ formula } ;}())`);

-   `function() { return ${ formula }; }`

This appears to be a template literal that creates an anonymous function. The formula variable seems to contain some expression or formula that's being interpolated into this function.

-   `eval(...)`

The entire template literal is passed into eval(), which attempts to execute the code within it as JavaScript.

This code snippet seems to be constructing a function dynamically based on the formula variable and then evaluating it using eval(). This approach can be powerful but may also pose security risks, especially if the formula variable contains `user input` or untrusted data.


## Attack Vector

Googling to refresh my memory I stumble upon this ineresting [article](https://medium.com/@sebnemK/node-js-rce-and-a-simple-reverse-shell-ctf-1b2de51c1a44).

In a nutshell, we can create an `attack vector` that depending on the case can use these two functions of the library '`fs`':

`readdir()` => Just as the dir command in MS Windows or the ls command on Linux, it is possible to use the method `readdir` or `readdirSync` of the fs class to list the content of the directory. 

`readFile()` => The methods `readFile` or `readFileSync` provide the option to read the entire content of a file.


<a id="org984ccea"></a>

## Payload

Now with these fixed concepts in mind let's go forge the payload.
For read `dir`.

    require('fs').readdirSync('..').toString()

![img](![folder](https://github.com/user-attachments/assets/f960834d-8e90-4385-ae47-b4d006a1f071)
)

For read `file`.

    require('fs').readFileSync('../flag.txt').toString()

![img](![file](https://github.com/user-attachments/assets/d0d206f2-9c58-4559-8a1e-654073a8b390)
)


## HTB{c4lcul4t3d_my_w4y_thr0ugh_rc3}
