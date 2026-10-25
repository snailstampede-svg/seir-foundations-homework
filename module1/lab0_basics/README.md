# EC2 Deployments from Launch Template

## Launch a new EC2 instance

    1. Select previously created launch template from the list and click *Actions*, *Launch instance from template*
    2. Verify settings populate and click *Launch instance*.
    3. Go to *Instances*, and wait for the instance state to show running.
    4. Wait for *Status check* to show as green 2/2 checks passed then Select instance created and click *Connect*
    5. In the Connect to Linux instance page, choose to connect *in web browser* and click *Connect*.

    | Deployment | Public IPv4 address | Connection method | Screenshot | Instance terminated? |
    |:-----------|:-------------------|:-----------------|:----------|:--------------------|
    | 1 | 54.210.231.134 | EC2 Connect | screenshots/deployment-1.png | Yes |
    | 2 | 98.82.184.88 | EC2 Connect | screenshots/deployment-2.png | Yes |
    | 3 | 3.82.2.108 | EC2 Connect | screenshots/deployment-3.png | Yes |

### Deployment 1

    Deployment 1 was launched from the Launch Template and I connected via EC2 Connect. The dashboard did not provide the public IP address of the instnace, however the EC2 Instance Connect window displayed the ip address (both public and private IPs) on the bottom banner along with the instance ID.

### Deployment 2

    After realizing that the information was available on the banner, I corrected my screenshots to include the instance connect banner.
### Deploynent
