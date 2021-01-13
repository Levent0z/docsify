# Clowder 

## How to get session ID for Gus

1. Login to gus.my.salesforce.com
2. In Developer Tools:
    a. Go to Application > Storage > Cookies > https://gus.lightning.force.com
    b. Sort cookies by name, find cookies with name 'sid'
    c. Get the value of the cookie with domain gus.my.salesforce.com
3. You can then use this value as a Bearer Token in Postman's Authorization tab


It should look like this: 00D0000000Dpvc!AQYAQ.....


