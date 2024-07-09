Note: if your shell prints a % at the end, leave that out when you copy the output.

1. You can use a simple network port forward to open port 8000 for Splunk Web access:
   
           kubectl port-forward splunk-s1-standalone-0 8000

2. Get your passwords for the namespace. The Splunk Enterprise passwords used in the namespace are generated automatically. To learn how to find and read the passwords, see the Reading global kubernetes secret object page.

3. Log into Splunk Enterprise at http://localhost:8000 using the admin account with the password.
