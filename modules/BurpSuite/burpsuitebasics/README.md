# Burp Suite: The Basics

> Vidath Dissanayake | 2021/09/31 | Sri Lanka
> [Room link](https://tryhackme.com/room/burpsuitebasics)
> [TryHackMe](https://tryhackme.com)

This is the first room of [Burp Suite](modules/BurpSuite/README.md) [module](modules/README.md). 

Here we get an introduction to [Burp Suite](modules/BurpSuite/README.md) as well as Proxy and Target modules.

---
---

## Task 1 [Introduction] Outline

**Instructions to start and access the box, as well as a room overview.**

1. Deploy the machine attached to the task by pressing the green "Start Machine" button, as well as the AttackBox (using the "Start AttackBox" button at the top of the page) if you are not using your own machine.  

    _**Note:** If you are not using the AttackBox and want to connect to this machine without the VPN, you can do so using this link once the machine has fully loaded and an IP address is displayed:_ [https://LAB_WEB_URL.p.thmlabs.com](https://lab_web_url.p.thmlabs.com/)
    
    > Just start the machine and access it through the given link.
    
    ```
    No answer needed
    ```

***Note: I will be using this method to access the website.***

---

## Task 2 [Getting Started] What is Burp Suite?

**A basic intro to Burp and it's editions.**

1. Which edition of Burp Suite will we be using in this module?

    > Read the description.

    ```
    Burp Suite Community
    ```

2. Which edition of Burp Suite runs on a server and provides constant scanning for target web apps?

    > Read the description.

    ```
    Burp Suite Enterprise
    ```

3. Burp Suite is frequently used when attacking web applications and ______ applications.

    > Read the description and fill in the blank.

    ```
    Mobile
    ```

---

## Task 3 [Getting Started] Features of Burp Community

**Intro to modules in Burp and extensions.**

1. Which Burp Suite feature allows us to intercept requests between ourselves and the target?

    > Read the description.

    ```
    Proxy
    ```

2. Which Burp tool would we use if we wanted to bruteforce a login form?

    > Read the description.

    ```
    Intruder
    ```

---

## Task 4 [Getting Started] Installation

**Installation instructions for Community Edition.**

1. If you have chosen not to use the AttackBox, make sure that you have a copy of Burp Suite installed before proceeding.

    ```
    No answer needed
    ```

---

## Task 5 [Getting Started] The Dashboard

**Intro to the Dashboard interface**

1. Open Burp Suite and have a look around the dashboard. Make sure that you are comfortable with it before moving on.

    ```
    No answer needed
    ```

---

## Task 6 [Getting Started] Navigation

**Instructions on how to navigate the GUI and common keyboard shortcuts for navigation.**

1. Get comfortable navigating around the top menu bars.

    ```
    No answer needed
    ```

---

## Task 7 [Getting Started] Options

**Instructions about managing User and Project Options.**

1. Change the Burp Suite theme to dark mode

    > This option can be found in User Options > Display > User Interface > Theme: Dark

    ```
    No answer needed
    ```

![Screenshot of option to turn on dark mode](assets/t7q1.png)

2. In which *Project Options* sub-tab can you find reference to a "Cookie jar"?

    > Go through the Project Options. You will find "Cookie jar" pretty easily.

    ```
    Sessions
    ```

![Screenshot of Cookie jar in Sessions sub-tab](assets/t7q2.png)

3. In which *User options* sub-tab can you change the Burp Suite update behaviour?

    > Again, browse through User Options.

    ```
    Misc
    ```

![Screenshot of Misc sub-tab](assets/t7q3.png)

4. What is the name of the section within the *User options* "Misc" sub-tab which allows you to change the Burp Suite key bindings?

    > Should be pretty obvious once you visit User Options > Misc.

    ```
    Hotkeys
    ```

![Screenshot of Hotkeys](assets/t7q4.png)

5. If we have uploaded Client-Side TLS certificates in the *User options* tab, can we override these on a per-project basis (Aye/Nay)?

    > Yes. Most User Options can be overridden in Project Options. You can find this specific option in Project Options > TLS > Client TLS Certificates > Override user options.

    ```
    Aye
    ```

![Screenshot of overriding uploaded Client-Side TLS certificates in User options via Project options](assets/t7q5.png)

6. There are many more configuration options available. Take the time to read through them.

    In the next section, we will cover the Burp Proxy -- a much more hands-on aspect of the room.

    ```
    No answer needed
    ```

---

## Task 8 [Proxy] Introduction to the Burp Proxy

**Intro to Proxy module, its sub-tabs and basic config.**

1. Which button would we choose to send an intercepted request to the target in Burp Proxy?

    > We "forward" the request.

    ```
    Forward
    ```

![Screenshot of forward button for captured request](assets/t8q1.png)

2. **[Research]** What is the default keybind for this?

    _**Note:** Assume you are using Windows or Linux (i.e. swap Cmd for Ctrl)._

    > You can find the keybinding by doing a simple google search or by looking at User Options > Misc > Hotkeys

    ```
    Ctrl+F
    ```

![Screenshot of the keybinding in Hotkeys](assets/t8q2.png)

---

## Task 9 [Proxy] Connecting through the Proxy (FoxyProxy)

**Instructions to install and configure FoxyProxy**

1. Read through the options in the right-click menu.

    There is one particularly useful option that allows you to intercept and modify the *response* to your request.

    What is this option?

    _**Note:** The option is in a dropdown sub-menu._

    > Go through the right-click menu and see what fits the description. It's Do intercept > Response to this request.

    ```
    Response to this request
    ```

![Screenshot showing position of answer in right click menu](assets/t9q1.png)

2. **[Bonus Question -- Optional]** Try installing FoxyProxy standard and have a look at the pattern matching features.

    > Have a go at this if you feel like it!

    ```
    No answer needed
    ```

---

## Task 10 [Proxy] Proxying HTTPS

**Instructions to set up HTTPS support for Burp Proxy**

1. If you are not using the AttackBox, configure Firefox (or your browser of choice) to accept the Portswigger CA certificate for TLS communication through the Burp Proxy.

    > Follow the given instructions and do this if needed.

    ```
    No answer needed
    ```

---

## Task 11 [Proxy] The Burp Suite Browser

**Intro to using and troubleshooting inbuilt browser.**

1. Using the in-built browser, make a request to `http://MACHINE_IP/` and capture it in the proxy.

    > Pretty self explanatory. Open the inbuilt browser with intercept on in Proxy and browse to `http://MACHINE_IP/`.

    ```
    No answer needed
    ```

![Screenshot of captured request from inbuilt browser](assets/t11q1.png)

---

## Task 12 [Proxy] Scoping and Targeting

**Instruction to configure scope in Target tab.**

1. Add `http://MACHINE_IP/` to your scope and change the Proxy settings to only intercept traffic to in-scope targets.

    See the difference between the amount of traffic getting caught by the proxy before and after limiting the scope.
    
    > Follow the instructions in the room to do this. You will notice that much less traffic is being captured specially if you have other tabs open.

    ```
    No answer needed
    ```

---

## Task 13 [Proxy] Site Map and Issue Definitions

**Intro to Target module and its sub-tabs.**

1. Take a look around the site on `http://MACHINE_IP/` -- we will be using this a lot throughout the module. Visit every page linked to from the homepage, then check your sitemap -- one endpoint should stand out as being very unusual!

    Visit this in your browser (or use the "Response" section of the site map entry for that endpoint)

    What is the flag you receive?
    
    > With intercept off in Proxy (but with the browser configured to send all traffic through the proxy), browse through the whole web site. (Click every link you find! I usually prefer to <kbd>Ctrl</kbd> + click all links to open in new tabs and close them each after reading through with <kbd>Ctrl</kbd> +<kbd>W</kbd>). Then check the site map. You will see a weird seemingly random file. Clicking on it reveals that it was referred by *http:/MACHINE_IP.p.thmlabs.com/ticket/* and a *GET* request was made to it. The response reveals the flag.

    ```
    THM{NmNlZTliNGE1MWU1ZTQzMzgzNmFiNWVk}
    ```

    ![Screenshot with flag from interesting endpoint](assets/t13q1.png)

2. Look through the Issue Definitions list.

    What is the typical severity of a Vulnerable JavaScript dependency?
    
    > Scroll down the Issue Definition list and find "Vulnerable Javascript Dependency".

    ```
    Low
    ```
    
    ![Screenshot showing Vulnerable Javascript Dependency](assets/t13q2.png)

---

## Task 14 [Practical] Example Attack

**Finally! A practical after all that theory!**

1. Try typing: `<script>alert("Succ3ssful XSS")</script>`, into the "Contact Email" field. You should find that there is a client-side filter in place which prevents you from adding any special characters that aren't allowed in email addresses:

    ![GIF demonstrating the client side filter](assets/t14q1.gif)
    
    ```
    No answer needed
    ```

2. Fortunately for us, client-side filters are absurdly easy to bypass. There are a variety of ways we could disable the script or just prevent it from loading in the first place.

    Let's focus on simply bypassing the filter for now.

    First, make sure that your Burp Proxy is active    and that the intercept is on.
    
    > You know how to do this.
    
    ```
    No answer needed
    ```
    
3. Now, enter some legitimate data into the support form. For example: "pentester@example.thm" as an email address, and "Test Attack" as a query.

    Submit the form -- the request should be intercepted by the proxy.
    
    > Self explanatory.

    ```
    No answer needed
    ```
    
4. With the request captured in the proxy, we can now change the email field to be our very simple payload from above:  
    `<script>alert("Succ3ssful XSS")</script>`. After pasting in the payload, we need to select it, then URL encode it with the `Ctrl + U` shortcut to make it safe to send. This process is shown in the GIF below:

    ![GIF demonstrating the explained process of intercepting and URL encoding the pasted payload](assets/t14q4.gif)

    > See the GIF. Replace the email with the payload and URL encode it by selecting it and pressing <kbd>Ctrl</kbd> + <kbd>U</kbd>

    ```
    No answer needed
    ```
    
5. Finally, press the "Forward" button to send the request.

    You should find that you get an alert box from the site indicating a successful XSS attack!

    ![Screenshot showing the successful XSS attack](assets/t14q5.png)

    > Press "Forward" button and check the browser. You should see a popup like shown above.

    ```
    No answer needed
    ```

6. Congratulations, you bypassed the filter!

    Don't expect it to be quite so easy in real life, but this should hopefully give you an idea of the kind of situation in which Burp Proxy can be useful.
    
    > Most websites have some form of XSS protection. So, it won't be this easy in real life.

    ```
    No answer needed
    ```

---

# Task 15 [Conclusion] Room Conclusion

**Room conclusion and link to the sequel to this room, [Burp Suite: Repeater](../burpsuiterepeater/README.md).**
  
1. I understand the fundamentals of using Burp Suite!

    > I sure hope you do, after such an informative room.

    ```
    No answer needed
    ```