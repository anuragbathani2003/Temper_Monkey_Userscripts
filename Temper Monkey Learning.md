
## 📄 Introduction to User scripts

**Userscripts** are small, client-side JavaScript programs that allow users to customize the behavior and appearance of websites. They run in the browser, usually through browser extensions like **Tampermonkey**, **Greasemonkey**, or **Violentmonkey**, and are executed when a page loads based on the URL patterns specified in the script.

These scripts empower users to:

- Modify webpage content dynamically
    
- Automate repetitive browser tasks
    
- Add new UI components or features to existing sites
    
- Extract and process data from web pages
    
- Bypass limitations or improve UX without changing the server-side code
    

A userscript typically includes:

- A **metadata block** that tells the browser where and when to run it
    
- JavaScript logic to manipulate the DOM, fetch data, or interact with the site
    

Because userscripts run only in the user's browser, they provide a lightweight and flexible method for personal web customization without affecting the server or requiring access to the original source code.

## some important keywords

These keywords are used inside the **metadata block** (`// ==UserScript== ... // ==/UserScript==`) at the top of each userscript. They define how and where the script will run.

---

### 1. `@name`

- **Purpose:** Sets the name of your userscript.
    
- **Example:** `@name My Custom Script`
    
- **Usage:** This name appears in the Tampermonkey dashboard.
    

---

### 2. `@namespace`

- **Purpose:** A unique identifier for the script author or project.
    
- **Example:** `@namespace http://tampermonkey.net/`
    
- **Usage:** Helps differentiate between scripts with the same name.
    

---

### 3. `@version`

- **Purpose:** Specifies the version number of the script.
    
- **Example:** `@version 1.0`
    
- **Usage:** Useful for script maintenance, updates, and debugging.
    

---

### 4. `@description`

- **Purpose:** Provides a short description of what the script does.
    
- **Example:** `@description Alerts "Hello World" on every page.`
    
- **Usage:** Shown in the Tampermonkey dashboard and update prompts.
    

---

### 5. `@author`

- **Purpose:** States the author of the script.
    
- **Example:** `@author John Doe`
    
- **Usage:** Optional but good for credit and contact reference.
    

---

### 6. `@match`

- **Purpose:** Specifies which websites/pages the script will run on.
    
- **Example:** `@match *://*.example.com/*`
    
- **Usage:** Supports wildcards (`*`) to match multiple domains or paths.
    

> Only URLs that match these patterns will trigger the script.

---

### 7. `@grant`

- **Purpose:** Requests access to special Tampermonkey functions (APIs).
    
- **Example:** `@grant GM_setValue`
    
- **Usage:**
    
    - `none`: No special permissions needed.
        
    - Common values:
        
        - `GM_setValue` / `GM_getValue` — for local storage
            
        - `GM_xmlhttpRequest` — for cross-site AJAX requests
            
        - `GM_download` — to programmatically download files
            

---

### 8. `@run-at` _(optional but useful)_

- **Purpose:** Defines when the script should run.
    
- **Example:** `@run-at document-end`
    
- **Options:**
    
    - `document-start`: before page starts loading
        
    - `document-end`: after DOM is ready
        
    - `document-idle`: after everything is fully loaded

# some example of user Scripts

## 1. basics of user script

### 1. print in console

```javascript
// ==UserScript==
// @name         My Custom Script
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    window.addEventListener('load', ()=> {
    console.log('Page Loaded successfully!');
    })
})();

```

it will wait until the entire page is loading once the page loaded then this even listener run callback function and its print in console ** Page Loaded successfully**

### 2. Log Url time and title

```javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
     window.addEventListener('load', ()=>{
     const url=window.location.href;
     const title=document.title;
     const currentTime= new Date().toLocaleString();

     console.log("==page info==");
     console.log("URL:",url);
     console.log("Title:",title);
     console.log("Time:",currentTime);
     });
})();
```

it will print all the urls Titles Time on console when the page is loaded 


### 3. set yellow color to all paragraph

```javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
     window.addEventListener('load', ()=>{
     const paragraph=document.querySelectorAll('p');
         paragraph.forEach(p => {p.style.backgroundColor='yellow';});

         console.log(`${paragraph.length} elements`);

     });
})();
```

it will select all the paragraph tag on the page and change the color of it to yellow 

### 4. button click listener

```javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    window.addEventListener('load', () => {
        const buttons = document.querySelectorAll('button');
        buttons.forEach((button, index) => {
            button.addEventListener('click', (event) => {
                console.log(`Button ${index + 1} Clicked.`);
            });
        });
    });
})();
```

it will get all the buttons in the webpage and log when button is clicked

### 5. auto  Refresh a page  in specific interval

```javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    const intervalinmili=60 * 1000;

    console.log(` this page is auto reload in every ${intervalinmili/1000} seconds`);
    setTimeout(() => {
    location.reload();},intervalinmili);

})();
```

it will refresh a page in every 60 seconds and also you can specify and modify the interval of the refreation

### 6. Delayed Welcome message

```javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
     setTimeout(() => {
     const banner=document.createElement('div');
         banner.innerText=" Welcome to This Page!!";
         banner.style.position = 'fixed';
         banner.style.top = '10px';
         banner.style.left = '50%';
         banner.style.tranform='translateX(-50%)';
         banner.style.background='#f0c674';
         banner.style.color = '#000';
         banner.style.padding = '10px 20px';
         banner.style.border = '2px solid #333';
         banner.style.borderRadius = '8px';
         banner.style.zIndex = '9999';
         banner.style.boxShadow = '0px 2px 6px rgba(0,0,0,0.3)';
          document.body.appendChild(banner);

         console.log(" Welcome to this Page!!!");
     },5000);

})();
```

create a custom banner that shows on a page after 5 second Delayed and also log in console 

### 7. find the particular word and replace it according to you

```javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
     window.addEventListener('load', () =>{
       const replacements={
        "JavaScript" : "JS",
        "TamperMonkey": "User Script Engine",
        "Google": "Search Engine",
        "unsafeWindow": "safeWindow"
       };

       function replaceText(node){

        if(node.nodeType == Node.TEXT_NODE){
            for(const [key, value] of Object.entries(replacements)){
                node.textContent =node.textContent.replace(new RegExp(key,'g'),value);
            }
        }
        else{
            node.childNodes.forEach(replaceText)
        }
       }

       replaceText(document.body);
       console.log("Text replacements applied.");

     });

})();

```

it find the words like javascript,google,unsafewindow on the page and replace it according to the map that we put in our script

### 8.Show Current Time in Page

```javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
     window.addEventListener('load',() =>{
        const orititle=document.title;
        setInterval(() => {
            const now=new Date();
            const timeString=now.toLocaleTimeString();

            document.title= `[${timeString}] ${orititle}`;

        }, 1000);
     })

})();
```

it will add the current time step to the title and refresh it in every 1 second so the real current time will shown in the title of the page


### 9. Scroll Progress Indicator

```javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
     // Create the progress bar element
    const progressBar = document.createElement('div');
    progressBar.style.position = 'fixed';
    progressBar.style.top = '0';
    progressBar.style.left = '0';
    progressBar.style.width = '0%';
    progressBar.style.height = '4px';
    progressBar.style.backgroundColor = '#29d';
    progressBar.style.zIndex = '9999';
    progressBar.style.transition = 'width 0.2s ease-out';
    document.body.appendChild(progressBar);

    //update progress on scroll

    window.addEventListener('scroll', () => {
        const scrollTop = window.scrollX || document.documentElement.scrollTop;
        const docHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight;
        const scrolled =(scrollTop/docHeight) *100;

        progressBar.style.width = `${scrolled}%`;

    })

})();
```

it will create a horizontal progress bar on any scrollable page and indicate a scrolled portion on progress bar

### 10. Auto-Fill a Search Box

```javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    const searchbox = document.querySelector('input[type="search"],input[name ="q"],input[placeholder*="search"]');

    if(searchbox){
        searchbox.value=' you are hacked';
        console.log('Search box auto-filled!');
    }
    else {
            console.log('No search box found.');
        }

})();
```

its find the search boxes in the page and autofill the search box with your input.


## 2. @match / @include / @exclude

### 1.Change Background Color on All Websites

```javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    document.body.style.backgroundColor = "#ff0000";
})();

```

change the background to body tag to red,

### 2. Auto Fill Login Form on a Specific Site

```javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    https://charusat.edu.in:912/eGovernance/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    document.querySelector('#txtUserName').value = 'anurag';
    document.querySelector('#txtPassword').value = '111003';

})();

```

auto fill the username and password on charusat egovernance login page.

### 3. Hide Sidebar on YouTube but Not on Shorts

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
	    // @include      https://www.youtube.com/*
    // @exclude      https://www.youtube.com/shorts/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
      const sidebar=document.getElementById('guide');
      if(sidebar) sidebar.style.display= 'none';


    })();
```

it will hide a side bar on youtube except shorts.

### 4. Change Font Style on Wikipedia Articles Only

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @include      https://en.wikipedia.org/wiki/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
       document.body.style.fontFamily = 'Comic Sans MS, cursive';
    })();
```

it change the font of wikipedia pages and only restricted to the wikipidia pages .

### 5. Redirect to to a perticuler url in youtube

```javascript
// ==UserScript==
// @name         Redirect All YouTube Pages to Shorts
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Redirects any YouTube page to a specific Shorts video
// @author       You
// @match        https://www.youtube.com/*
// @grant        none
// @run-at       document-start
// ==/UserScript==

(function() {
    'use strict';

    // Specify the Shorts video URL you want to redirect to
    const shortsURL = 'https://www.youtube.com/shorts/SWT9arb8Hxk';

    function redirectToShorts(){
        if (window.location.href !== shortsURL) {
        window.location.replace(shortsURL);
    }
    }

    redirectToShorts();
    setInterval(redirectToShorts,2000);



})();
```

in youtube if you go to any page it will redirect to the perticuler short 


### 6. Change the github all pages background except gist pages

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        https://github.com/*
    // @exclude      https://gist.github.com/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
       const style=document.createElement('style');
       style.innerHTML = `body{background-color : #ff00ff;}`;
       document.head.appendChild(style);


    })();

```

it will change a background color of all github pages except if the url not start with gist subdomain

### 7. High light all present link on wikipedia

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @include      https://en.wikipedia.org/wiki/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
      const links=document.querySelectorAll('a');

      links.forEach(link => {
        link.style.backgroundColor ='yellow';
      });


    })();

```

it will highlight all the links on wikipedia.

### 8. focus on the search box in amazon

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        https://www.amazon.com/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
         const searchBox = document.getElementById('twotabsearchtextbox');
    if (searchBox) searchBox.focus();
    })();
```


when you open a amazon it will focus the search button.

### 9. redirection shorts to standard video format

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        https://www.youtube.com/shorts/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
   const videoId = window.location.pathname.split('/').pop();
    window.location.href = `https://www.youtube.com/watch?v=${videoId}`;
    })();

```

if you open any shorts on youtube it will redirect to standard video of youtube.

### 10. Remove cookie banner from w3school

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        https://www.w3schools.com/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
        
        
    const interval = setInterval(() => {
        const banner = document.getElementById('accept-choices');
        if (banner) {
            banner.remove();
            clearInterval(interval); 
        }
    }, 500); // Check every 500ms
    })();

```

it will remove a cookie consent bar from the w3school and check in every 0.5 second if its find then remove it 


## 3.cookie and localstorage releted userscript


### 1. create a test cookie

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
document.cookie = "testCookie=12345;path=/;";


    })();
```

create a test cookie which accessble in whole application.

### 2. print all cookie in alert box

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
     alert("Cookies :" + document.cookie);


    })();

```

print all the cookie in alert box

### 3. update the value of particular cookie

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
    document.cookie = "sessionId=9999;path=/;";


    })();

```

its update a sessionId=9999 and you can modify any cookie value like this

### 4. Check if User cookie is present or not

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
      if(document.cookie.includes("user=")){
        alert("the user cookie exists!!");

      }
      else{
        alert("the user cookie is not exists");
      }
    })();

```

if the website contain user cookie that the alert will generate 

### 5.  Replace a cookie values

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
       document.cookie.split(";").forEach(cookie => {
            const name=cookie.split("=")[0].trim();
            document.cookie=`${name} =dummy;path=/;`;
       });
    })();

```

it will fetch all the accessble cookie from the javascript and modify the value to "dummy".

### 6. check a particular token or key is present or not in localstorage

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
       const token=localStorage.getItem('__lsv__');

       if(token){
        alert('__lsv__ = ' + token);
       }
       else{
        alert('__lsv__ not found...');
       }
    })();
```

it will check a  a lsv token is present or not in the localstorage and generate according alert in that

### 7. Remove a Particular Item

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
       localStorage.removeItem('__lsv__');
    })();

```

remove __lsv__ from localstorage

### 8. Check a particular item and if not exists than create one

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
        if (!localStorage.getItem('loginStatus')) {
        localStorage.setItem('loginStatus', 'false');
    }
    })();
```

check for particular item if its dont exists then create one

### 9.clear the localStorage

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
        localStorage.clear();
    })();

```

it will clear the localstorage 


### 10.  auto update a counter when page refresh

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        none
    // ==/UserScript==

    (function() {
        'use strict';
            let count = parseInt(localStorage.getItem('mycount'));
    if (isNaN(count)) count = 0;
    count++;
    localStorage.setItem('mycount', count);
    console.log(`mycount: ${count}`);
    })();

```

it will check first if mycount is present in localstorage or not if it found present it will simply increment by one and update the value in local storage and if it dont find the my count key so it will create one with the value 1 



## 4.  GM_APIs of Tempermonkey


### 1. take a user input and store it when the page is reload the alert is shown

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        GM_setValue
    // @grant        GM_getValue
    // ==/UserScript==

   (async () => {
  let name = await GM_getValue("username");
  if (!name) {
    name = prompt("What is your name?");
    if (name) {
      await GM_setValue("username", name);
    }
  }
  if (name) alert(`Welcome back, ${name}!`);
})();

```

it will get the username from the storage if username is not present then take  a username and stored it and when the page reload it will show a alert with welcome message.

### 2. fetch a joke from cross-origin

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        GM_setValue
    // @grant        GM_getValue
    // @grant        GM_xmlhttpRequest
    // ==/UserScript==

    GM_xmlhttpRequest({
  method: "GET",
  url: "https://official-joke-api.appspot.com/random_joke",
  onload: function(response) {
    const joke = JSON.parse(response.responseText);
    alert(`${joke.setup} - ${joke.punchline}`);
  }
});

```

fetch a random joke from free joke api and wshow in alert

### 3. create a button that download a image

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        GM_setValue
    // @grant        GM_getValue
    // @grant        GM_download
    // ==/UserScript==

    (function() {
        'use strict';

        document.querySelectorAll("img").forEach((img, i) => {
  const btn = document.createElement("button");
  btn.textContent = "Download";
  btn.style.display = "block";
  btn.onclick = () => GM_download(img.src, `image-${i}.jpg`);
  img.after(btn);
});
    })();

```

it will create a download button after every image that apper on the page and user can download any image 

### 4. change a background color with GM 

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        GM_addStyle
    // ==/UserScript==

    (function() {
        'use strict';

        GM_addStyle("body { background-color: lightblue !important; }");
       })();

```

change the background color

### 5. reset a any variable 

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        GM_registerMenuCommand
    // @grant        GM_setValue
    // @grant        GM_getValue
    // ==/UserScript==


    GM_registerMenuCommand("Reset the name",async () => {

        await GM_setValue("username" , "anurag");

        alert(`the name was reseting to ${await GM_getValue("username")}`);
    });


```

this script will reset a username parameter to anurag.and generate alert


### 6. how to use a external library in your script

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @grant        GM_registerMenuCommand
    // @grant        GM_setValue
    // @require      https://code.jquery.com/jquery-3.6.0.min.js
    // ==/UserScript==


   $(document).ready(function() {
  console.log("jQuery version:", $.fn.jquery);
});


```

it will load a jquery in the script and log the version of it to verify the library is successfully loded or not

### 7. control to when the script is run

```javascript

    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @run-at       document-end
    // ==/UserScript==

    console.log("This runs after the page has loaded.");
```

it runs when the page is fully loaded

### 8.load external resource into the webpage

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // @resource     sampleImage https://static.macupdate.com/products/7899/m/simpleimage-logo.webp?v=1568294417
    // @grant        GM_getResourceURL
    // ==/UserScript==

    (function() {
  const imgURL = GM_getResourceURL("sampleImage");
  const img = document.createElement("img");
  img.src = imgURL;
  img.style.width = "100px";
  document.body.appendChild(img);
})();

```

it will load a external resource as a image to the current webpage
### 9. create atoggle menu which can toggle a light theme and dark theme of a webpage

``` javascript
// ==UserScript==
// @name         Console log on every page
// @namespace    http://tampermonkey.net/
// @version      1.1
// @description  Alert "Hello World" on example.com
// @author       You
// @match        *://*/*
// @grant        GM_setValue
// @grant        GM_getValue
// @grant        GM_addStyle
// @grant        GM_registerMenuCommand
// ==/UserScript==

(async function () {
    'use strict';

    // Get current theme from storage
    let currentTheme = await GM_getValue("theme", "light");

    const darkThemeCSS = `
        body {
            background-color: #121212 !important;
            color: #e0e0e0 !important;
        }
        a { color: #80cbc4 !important; }
    `;

    const lightThemeCSS = `
        body {
            background-color: #ffffff !important;
            color: #000000 !important;
        }
        a { color: #1a0dab !important; }
    `;

    // Apply the appropriate theme
    if (currentTheme === "dark") {
        GM_addStyle(darkThemeCSS);
    } else {
        GM_addStyle(lightThemeCSS);
    }

    // Theme toggle function
    async function toggleTheme() {
        const updatedTheme = currentTheme === "dark" ? "light" : "dark";
        await GM_setValue("theme", updatedTheme);
        alert(`Theme changed to ${updatedTheme}`);
        location.reload(); // Reload to apply new theme
    }

    // Register menu command to toggle theme
    GM_registerMenuCommand("Toggle Theme", toggleTheme);
})();

```

its use a temper monkeys special apis and make a toggle manu in tampermonkeys extension which can toggle a theme between dark and light 


### 10.  preserve artical scroll and restore when reload

```javascript
// ==UserScript==
// @name         Article Scroll Tracker
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @author
// @match        https://example.com/*
// @grant        GM_setValue
// @grant        GM_getValue
// ==/UserScript==

(async function () {
    'use strict';

    const pageKey = `scrollPosition_${location.pathname}`; // unique key per article URL

    // Restore scroll position on load
    const savedPosition = await GM_getValue(pageKey, 0);
    window.scrollTo(0, savedPosition);

    // Throttle function to avoid saving too frequently
    function throttle(fn, delay) {
        let lastCall = 0;
        return function (...args) {
            const now = Date.now();
            if (now - lastCall >= delay) {
                lastCall = now;
                return fn(...args);
            }
        };
    }

    // Save scroll position every 1 second while scrolling
    const saveScroll = throttle(() => {
        GM_setValue(pageKey, window.scrollY);
    }, 1000);

    window.addEventListener('scroll', saveScroll);
})();

```

it will first save the current scroll and also create a page key for every diffrent pages  then it stores the vertical page scroll in every one second and there is special function to called throttle that restrict a frequent storage of the scroll and make sure the function called exactly after one second




## 5. data extraction with some advanced concepts

### 1. when DOM changed this will log the changes 

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // ==/UserScript==

    const observer=new MutationObserver((mutations) => {
        console.log("dom changed..",mutations);
    });

    observer.observe(document.body,{childList : true,subtree: true});




```

in this script there is a mutation observer is their when the dom is changed so it will log in console 

### 2. fetch a joke from fetch 

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
    // ==/UserScript==


fetch('https://v2.jokeapi.dev/joke/Any?type=single')
    .then(res => res.json())
    .then(data => {
        console.log(" a joke:", data.joke);
    })
```

it will fetch a  joke from  the api and log it on console

### 3.  fetch a joke with axios api

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
  // @require      https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js
// ==/UserScript==

axios.get('https://v2.jokeapi.dev/joke/Any?type=single')
    .then(response => {
        console.log("Joke API result ==> ", response.data.joke);
    })
```

it will fetch a joke as above but with diffrent method like axios because axios is vvery easy to render a json responces 

### 4.  auto click button 

```javascript

    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
// ==/UserScript==


const btn = document.querySelector('button');
if (btn) {
    console.log("Clicking button:", btn.innerText);
    btn.click();
}

```

it will click a very first button on the webpage and also log in the console.

### 5. auto click a signup button

```javascript
    // ==UserScript==
    // @name         Console log on every page
    // @namespace    http://tampermonkey.net/
    // @version      1.0
    // @description  Alert "Hello World" on example.com
    // @author       You
    // @match        *://*/*
// ==/UserScript==

window.addEventListener('load', () => {
    const signUpBtn = Array.from(document.querySelectorAll('button, input[type="button"], input[type="submit"]'))
        .find(el => el.textContent?.trim().toLowerCase() === 'sign up' || el.value?.trim().toLowerCase() === 'sign up');

    if (signUpBtn) {
        console.log("Clicking 'Sign up' button:", signUpBtn);
        signUpBtn.click();
    } else {
        console.warn("'Sign up' button not found.");
    }
});
```

find a sign up button from the inner text of button and if the button is present then the button is clicked

### 6.  idenfify treditional popups and remove it

```javascript

// ==UserScript==
// @name         Amazon Special Offer Log
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @match        *://*/*
// @grant        none
// ==/UserScript==

const interval = setInterval(() => {
    const popup = document.querySelector('.modal, .popup, .overlay');
    if (popup) {
        popup.remove();
        console.log("Popup removed:", popup);
        clearInterval(interval);
    }
}, 1000);
```

this script identify classic popup s name and if find then remove it

### 7. find external urls  and bound with dased with box

```javascript
// ==UserScript==
// @name         Amazon Special Offer Log
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @match        *://*/*
// @grant        none
// ==/UserScript==

const currentHost = location.hostname;
const links = document.querySelectorAll('a[href]');
links.forEach(link => {
    if (!link.href.includes(currentHost)) {
        link.style.border = '2px dashed red';
        link.title = 'External Link';
    }
});
```

it will find a external urls and bound with dased box .


### 8 .it will create a help button on the bottom right corner

```javascript
// ==UserScript==
// @name         Amazon Special Offer Log
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Alert "Hello World" on example.com
// @match        *://*/*
// @grant        none
// ==/UserScript==

const btn = document.createElement('button');
btn.textContent = 'Help';
btn.style.position = 'fixed';
btn.style.bottom = '20px';
btn.style.right = '20px';
btn.style.zIndex = 10000;
btn.style.padding = '10px';
btn.style.backgroundColor = '#0af';
btn.style.color = '#fff';
btn.style.border = 'none';
btn.style.borderRadius = '8px';
btn.onclick = () => alert('This is your help panel.');
document.body.appendChild(btn);
```


### 9 . greb the video files url from the webpages

```javascript
// ==UserScript==
// @name         Video File Grabber
// @namespace    http://tampermonkey.net/
// @version      1.1
// @description  Extract and list all video files from the current page for download
// @match        *://*/*
// @grant        none
// @run-at       window.onload
// ==/UserScript==

(function () {
    'use strict';

    function getVideoURLs() {
        const urls = new Set();

        // <video src="">
        document.querySelectorAll('video[src]').forEach(video => {
            if (video.src) urls.add(video.src);
        });

        // <video><source src=""></video>
        document.querySelectorAll('video source[src]').forEach(source => {
            if (source.src) urls.add(source.src);
        });

        // <source src=""> (standalone, if any)
        document.querySelectorAll('source[src]').forEach(source => {
            const src = source.src;
            if (src && /\.(mp4|webm|ogg|mov|mkv)(\?|$)/i.test(src)) {
                urls.add(src);
            }
        });

        return Array.from(urls);
    }

    function createDownloadPanel(videoUrls) {
        const panel = document.createElement('div');
        panel.style.position = 'fixed';
        panel.style.top = '10px';
        panel.style.right = '10px';
        panel.style.background = 'white';
        panel.style.border = '2px solid #333';
        panel.style.padding = '10px';
        panel.style.zIndex = 99999;
        panel.style.maxHeight = '400px';
        panel.style.overflowY = 'auto';
        panel.style.fontFamily = 'monospace';

        const title = document.createElement('div');
        title.innerHTML = `<strong>🎥 Video Files Found (${videoUrls.length})</strong><br><br>`;
        panel.appendChild(title);

        videoUrls.forEach(url => {
            const link = document.createElement('a');
            link.href = url;
            link.textContent = url.split('/').pop().split('?')[0] || url;
            link.download = '';
            link.target = '_blank';
            link.style.display = 'block';
            link.style.marginBottom = '6px';
            panel.appendChild(link);
        });

        const closeBtn = document.createElement('button');
        closeBtn.textContent = 'Close';
        closeBtn.style.marginTop = '8px';
        closeBtn.onclick = () => panel.remove();
        panel.appendChild(closeBtn);

        document.body.appendChild(panel);
    }

    const videoUrls = getVideoURLs();
    if (videoUrls.length > 0) {
        createDownloadPanel(videoUrls);
    } else {
        console.log("No video files found.");
    }
})();
```



### 10 .add a animated view on the webpage

```javascript
// ==UserScript==
// @name         Special Offer Log
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description Alert "Hello World" on example.com
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function () {
    // Create the banner div
    const banner = document.createElement("div");
    banner.textContent = "🚀 Hello from Tampermonkey!";
    banner.style.position = "fixed";
    banner.style.top = "20px";
    banner.style.right = "20px";
    banner.style.padding = "10px 20px";
    banner.style.backgroundColor = "#6200ea";
    banner.style.color = "white";
    banner.style.borderRadius = "12px";
    banner.style.fontSize = "16px";
    banner.style.boxShadow = "0 4px 12px rgba(0,0,0,0.2)";
    banner.style.zIndex = "9999";
    banner.style.animation = "slide-fade 2s ease-in-out infinite alternate";

    // Add animation styles
    const style = document.createElement("style");
    style.textContent = `
        @keyframes slide-fade {
            0% {
                transform: translateY(0px);
                opacity: 1;
            }
            100% {
                transform: translateY(10px);
                opacity: 0.8;
            }
        }
    `;
    document.head.appendChild(style);
    document.body.appendChild(banner);
})();
```

it will create a animated view on top right corner on the webpage with the text = welcome to temper monkey




