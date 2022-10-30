# SEED-Labs-Cross-Site-Scripting-Attack-Lab-
Task 1: Posting a Malicious Message to Display an Alert Window
The objective of this task is to embed a JavaScript program in your Elgg profile, such that when another
user views your profile, the JavaScript program will be executed and an alert window will be displayed. The
following JavaScript program will display an alert window:
If you embed the above JavaScript code in your profile (e.g. in the brief description field), then any user
who views your profile will see the alert window.
In this case, the JavaScript code is short enough to be typed into the short description field. If you want
to run a long JavaScript, but you are limited by the number of characters you can type in the form, you can
store the JavaScript program in a standalone file, save it with the .js extension, and then refer to it using the
src attribute in the <script> tag. See the following example: 

Task 2: Posting a Malicious Message to Display Cookies
The objective of this task is to embed a JavaScript program in your Elgg profile, such that when another
user views your profile, the user’s cookies will be displayed in the alert window. This can be done by adding
some additional code to the JavaScript program in the previous task: 

Task 3: Stealing Cookies from the Victim’s Machine
In the previous task, the malicious JavaScript code written by the attacker can print out the user’s cookies,
but only the user can see the cookies, not the attacker. In this task, the attacker wants the JavaScript code to
send the cookies to himself/herself. To achieve this, the malicious JavaScript code needs to send an HTTP
request to the attacker, with the cookies appended to the request.
We can do this by having the malicious JavaScript insert an <img> tag with its src attribute set to the
attacker’s machine. When the JavaScript inserts the img tag, the browser tries to load the image from the
URL in the src field; this results in an HTTP GET request sent to the attacker’s machine. The JavaScript
given below sends the cookies to the port 5555 of the attacker’s machine (with IP address 10.9.0.1),
where the attacker has a TCP server listening to the same port. 

Task 4: Becoming the Victim’s Friend
In this and next task, we will perform an attack similar to what Samy did to MySpace in 2005 (i.e. the Samy
Worm). We will write an XSS worm that adds Samy as a friend to any other user that visits Samy’s page.
This worm does not self-propagate; in task 6, we will make it self-propagating.
In this task, we need to write a malicious JavaScript program that forges HTTP requests directly from
the victim’s browser, without the intervention of the attacker. The objective of the attack is to add Samy as
a friend to the victim. We have already created a user called Samy on the Elgg server (the user name is
samy).

Task 5: Modifying the Victim’s Profile
The objective of this task is to modify the victim’s profile when the victim visits Samy’s page. Specifically,
modify the victim’s "About Me" field. We will write an XSS worm to complete the task. This worm does
not self-propagate; in task 6, we will make it self-propagating.
Similar to the previous task, we need to write a malicious JavaScript program that forges HTTP requests
directly from the victim’s browser, without the intervention of the attacker. To modify profile, we should
first find out how a legitimate user edits or modifies his/her profile in Elgg. More specifically, we need
to figure out how the HTTP POST request is constructed to modify a user’s profile. We will use Firefox’s
HTTP inspection tool. Once we understand how the modify-profile HTTP POST request looks like, we can
write a JavaScript program to send out the same HTTP request. We provide a skeleton JavaScript code that
aids in completing the task. 


Task 6: Writing a Self-Propagating XSS Worm
To become a real worm, the malicious JavaScript program should be able to propagate itself. Namely,
whenever some people view an infected profile, not only will their profiles be modified, the worm will also
be propagated to their profiles, further affecting others who view these newly infected profiles. This way,
the more people view the infected profiles, the faster the worm can propagate. This is exactly the same
mechanism used by the Samy Worm: within just 20 hours of its October 4, 2005 release, over one million
users were affected, making Samy one of the fastest spreading viruses of all time. The JavaScript code that
can achieve this is called a self-propagating cross-site scripting worm. In this task, you need to implement
such a worm, which not only modifies the victim’s profile and adds the user “Samy” as a friend, but also
add a copy of the worm itself to the victim’s profile, so the victim is turned into an attacker. 

Task 7: Defeating XSS Attacks Using CSP
The fundamental problem of the XSS vulnerability is that HTML allows JavaScript code to be mixed with
data. Therefore, to fix this fundamental problem, we need to separate code from data. There are two ways to
include JavaScript code inside an HTML page, one is the inline approach, and the other is the link approach.
The inline approach directly places code inside the page, while the link approach puts the code in an external
file, and then link to it from inside the page. 


