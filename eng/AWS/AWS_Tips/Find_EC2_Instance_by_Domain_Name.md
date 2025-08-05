# Find EC2 Instance by Domain Name

> Sharing the method to find which EC2 instance a domain belongs to when you don't know

<br>

<br>

### 1. Go to Route 53 Console

- **Hosted zones**
  - Search url
  - Copy address from `Value/Route traffic to`

<br>

### 2. Go to EC2 Console

- **Load Balancers**
  - From the url copied above
    - Remove Internal prefix and trailing dot and search
  - Select `Listeners` tab
    - Click ~~~ from Default: forwarding to ~~~~~~
- **Target groups**
  - Found the instance!!!!

<br> 
