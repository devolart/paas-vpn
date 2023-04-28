<h1 align="center">PaaS VPN</h1>
<h2 align="center">Easily spin up an ephemeral VPN on Paas via Docker using tailscale under the hood</h2><br>

### Disclaimer:
<code>NEITHER me NOR this project shall be in any way held responsible if YOUR ACCOUNT gets banned. It is YOUR sole
reponsibility to use this project in whatever way you may want. However I totally recommend AGAINST ABUSING these 
services with excessive usage.</code><br>
### Prerequisites:
- Any PaaS with Docker image support (whether building from GitHub repositories or public docker images)
- Free [Tailscale](https://tailscale.com/) account<br>
### Pre Deployment Guide:
1. Signup on [Tailscale](https://tailscale.com/).

    ![1](/assets/1.png)
    ![2](/assets/2.png)
2. Connect atleast one device following the tailscale **Introduction guide**.

    ![3](/assets/3.png)
3. Go to the **Access Controls** tab and save the following JSON into **Edit file** section, replacing <code>email</code>
with the email shown in **Users** tab (if you use GitHub login, then it will be different. Please keep that in mind).
    ```json
    {
        "acls": [
          { "action": "accept", "src": ["*"], "dst": ["*:*"] },
        ],
        "tagOwners": {
          "tag:vpn": ["email"],
        },
        "autoApprovers": {
          "exitNode": ["tag:vpn"],
        }
    }
    ```

    ![4](/assets/4.png)
    ![7](/assets/7.png)
4. Go to **Keys** section in **Settings** tab and generate an **auth key**. Paste this key into the auth key variable when asked for.
Also save it for future use.

    ![5](/assets/5.png)
    ![6](/assets/6.png)<br>
### Deployment:
1. Point your PaaS deployment to this GitHub repo (or fork it if needed) or this public docker image `paasvpn/paasvpn`.
2. Set these environment variables.

`TAILSCALE_AUTHKEY`: Your auth key

`HOSTNAME`: Unique identifier for the VPN instance (you can fill some random string here)

`PORT` (Optional): Port for the front-end web interface. If you're not sure, try not using this first. If it doesn't work, try using 8080 port.
### Post Deployment guide:
1. Open tailscale client on the device you want to use VPN. (Guide shows for android)

    ![A](/assets/A.jpeg)
2. Connect your client to tailscale.
3. Tap **Use exit node** and select the correct online machine after checking in tailscale [dashboard](https://login.tailscale.com/admin/machines)

    ![B](/assets/B.jpeg)
    ![C](/assets/C.jpeg)
4. VPN should start working.

    ![D](/assets/D.jpeg)<br>
### Notes:
- Make sure, you have followed the steps as precisely as possible.
- **[Tailscale](https://tailscale.com/)** is a great tool in itself with extensive documention, make sure to try it.<br>
### Credit:
- [Mishizu](https://t.me/mishizu) for the original repository
