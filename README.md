# load-balancer-with-nginx
A step-by-step DevOps guide to configuring Nginx as a Layer 7 load balancer on Ubuntu. Features local DNS mapping using /etc/hosts, upstream server pooling, and HTTP/HTTPS traffic distribution for scalable web infrastructure.

<img width="554" height="94" alt="image" src="https://github.com/user-attachments/assets/f1251ce5-8364-4dee-b8b2-671442f50960" />

My first step for this project was to create an instance named nginxlb. 

<img width="554" height="143" alt="image" src="https://github.com/user-attachments/assets/bf875496-65ed-4d2a-b621-b4cde990f85a" />

I edited inbound rules and opened port 80 to allow HTTP connections, and I opened port 443 to secure HTTPS connections.

<img width="554" height="30" alt="image" src="https://github.com/user-attachments/assets/846f0dd5-5f24-4726-8307-286bf3590fce" />

I had to restart web1 and web2 but in the process webs erver 2 could not start meaning I had to change instance type from t3micro to t3small

<img width="554" height="218" alt="image" src="https://github.com/user-attachments/assets/cbe3e54c-1cb3-4cad-b50f-3343abcf02ff" />


<img width="130" height="132" alt="image" src="https://github.com/user-attachments/assets/81f0e6a7-7b01-424d-88c8-b287f6056ecc" />

I ssh into all 3 servers the nginx server and web server 1 and 2

<img width="465" height="280" alt="image" src="https://github.com/user-attachments/assets/470cf4d4-f660-4a08-84bd-dfc2ba8cd053" />

I opened my nginx lb server and used the command sudo nano /etc/hosts to open my /etc/hosts so it can be edited.

<img width="467" height="225" alt="image" src="https://github.com/user-attachments/assets/52cc0fdd-a27a-4236-a246-6315aca765f6" />

I used the commands  ping -c 2 Web1 & ping -c 2 Web2 to test if  local name resolution (DNS) between my Nginx Load Balancer server and the target web servers (Web1 and Web2). 

<img width="554" height="403" alt="image" src="https://github.com/user-attachments/assets/44a35da8-2236-40e5-9ea9-f24ed3b29ac8" />

My next step is to install latest packages using sudo apt update

<img width="553" height="341" alt="image" src="https://github.com/user-attachments/assets/7cfe4ba1-fb02-4f4b-859c-624dcdb00dd2" />

Next I installed nginx using sudo apt install nginx

<img width="554" height="298" alt="image" src="https://github.com/user-attachments/assets/9d37580b-27ef-4dfc-8cb8-8981d2d97cea" />

Next step is to configure  Nginxlb

<img width="554" height="217" alt="image" src="https://github.com/user-attachments/assets/e88bdfb3-b25b-42a3-b6df-d1a21d129d5b" />

I restarted Nginx to see if the  sysyem is running

<img width="554" height="132" alt="image" src="https://github.com/user-attachments/assets/9180285a-6b20-454f-b423-f8c221e42d74" />

Next step  is to set up my website on hostinger

<img width="554" height="198" alt="image" src="https://github.com/user-attachments/assets/9f84ba47-881b-483e-9c2f-6619bf1c49eb" />

Next step is to manage my domain

<img width="313" height="218" alt="image" src="https://github.com/user-attachments/assets/66bc9f0b-9a12-45d7-b771-a67ec8d11c1f" />

Next step is to allocate elastic IP address for my domain

<img width="554" height="226" alt="image" src="https://github.com/user-attachments/assets/c6b30b0b-8167-4e1d-83af-3c7364e0bbcd" />


<img width="553" height="189" alt="image" src="https://github.com/user-attachments/assets/dc848c6b-7f0a-4745-834d-f008a9cab7be" />

Next I had to associate my elastic IP address with my nginxlb

<img width="554" height="216" alt="image" src="https://github.com/user-attachments/assets/05e59167-cc48-4e9a-9280-e5b1ba0593d9" />

I edited my A record to my elastic IP address

<img width="553" height="170" alt="image" src="https://github.com/user-attachments/assets/86de11f6-ae30-469b-a63f-9db00388fe15" />

This is the updated record

<img width="310" height="258" alt="image" src="https://github.com/user-attachments/assets/62c866d8-cd75-4ee8-946a-a5ee1266827a" />

This shows that I have successfully connected my real Hostinger domain

<img width="554" height="98" alt="image" src="https://github.com/user-attachments/assets/714ef895-b567-4163-8555-d42adf3a9b6b" />

The old IP address timed out as a result I had to add new elastic IP address 16.170.38.44

<img width="528" height="550" alt="image" src="https://github.com/user-attachments/assets/67002589-74ac-489c-ac0b-b733f8f07f67" />

I used sudo nginx-t to test if there is no errors in my configuration file then sudo cat /etc/nginx/nginx.conf to see the contents of the file.

<img width="459" height="239" alt="image" src="https://github.com/user-attachments/assets/3f00d19e-5b67-4d92-8972-687637e26a51" />

I changed my server name from www.domain.com to www.prewebsite.online 

<img width="554" height="441" alt="image" src="https://github.com/user-attachments/assets/97df3fda-b6aa-4362-b91a-77be79904680" />

I tested connectivity from the Nginx load balancer to both backend web servers using the curl command. Web Server 1 successfully returned “Hello from Web Server 1”, confirming that the load balancer can reach the first backend server. Web Server 2 also responded successfully; however, it returned the default Red Hat Enterprise Linux HTTP test page because the server has not yet been configured with the project's custom web page. This confirms that network connectivity between the Nginx load balancer and both backend servers is working correctly, while Web Server 2 still requires web content configuration.

<img width="300" height="206" alt="image" src="https://github.com/user-attachments/assets/a1c3941c-9336-432f-a1ef-f23723225342" />

<img width="553" height="216" alt="image" src="https://github.com/user-attachments/assets/58311e57-8572-46c1-a41c-a3b57cee2927" />

While configuring Web Server 2, I attempted to edit the web page using the nano text editor with the command sudo nano /var/www/html/index.html. However, the command initially failed because Nano was not installed on the server. I then installed Nano using the RHEL package manager with the command sudo dnf install nano -y. The installation successfully resolved and downloaded the Nano package from the configured RHEL repository, allowing me to continue editing the web server's HTML content.

<img width="481" height="229" alt="image" src="https://github.com/user-attachments/assets/1083fba0-0252-4c95-a12a-5a799aee51b1" />

After installing Nano on Web Server 2, I created an index.html file in the /var/www/html/ directory using sudo nano /var/www/html/index.html. I added a simple HTML page displaying “Hello from Web Server 2” and then restarted the Apache HTTP server using sudo systemctl restart httpd to apply the changes. I verified that the configuration was working by running curl http://172.31.33.41, which successfully returned the HTML content containing “Hello from Web Server 2”. This confirmed that Web Server 2 was correctly serving its custom webpage and was ready to receive requests from the Nginx load balancer.

<img width="554" height="191" alt="image" src="https://github.com/user-attachments/assets/486f4fc5-60ad-4282-bf7c-d456a8d0e6d9" />

I tested connectivity from the Nginx Load Balancer to both backend web servers using the curl command. The request to Web Server 1 at 172.31.46.146 successfully returned “Hello from Web Server 1”, while the request to Web Server 2 at 172.31.33.41 successfully returned the HTML page containing “Hello from Web Server 2.” This confirmed that both backend web servers are accessible from the Nginx Load Balancer and are correctly serving their respective web content. Therefore, both servers are ready to participate in the Nginx load-balancing configuration.

<img width="554" height="385" alt="image" src="https://github.com/user-attachments/assets/dfb65077-94f9-4b9f-92f2-3f792bae1235" />

I tested the Nginx load balancer using the registered domain prewebsite.online by sending multiple HTTP requests with the curl command. The requests were successfully distributed between Web Server 1 and Web Server 2. Some requests returned “Hello from Web Server 1”, while others returned the HTML content displaying “Hello from Web Server 2.” This confirmed that the Nginx load balancer is successfully distributing incoming requests across both backend web servers using the configured upstream myproject. Both backend servers are therefore functioning correctly behind the Nginx load balancer.

<img width="554" height="326" alt="image" src="https://github.com/user-attachments/assets/558d4cb2-fd44-407c-ae1e-246fe9d020b1" />

Certbot was installed on the Nginx load balancer to enable HTTPS and secure communication for the registered domain. The python3-certbot-nginx package was also installed to allow Certbot to integrate with and configure the Nginx web server.

<img width="324" height="55" alt="image" src="https://github.com/user-attachments/assets/d4e8a16c-fcd2-4ec1-9cf7-1c0476269607" />

Next was to check certbot version

<img width="554" height="310" alt="image" src="https://github.com/user-attachments/assets/4da7d7f0-128f-44ce-bf40-b11e6b63bf53" />

I verified that the Nginx configuration was valid by running sudo nginx -t, which returned “syntax is ok” and “test is successful.” I also confirmed that the Nginx service was active and running using sudo systemctl status nginx. I then used Certbot with the Nginx plugin to obtain an SSL/TLS certificate for prewebsite.online and www.prewebsite.online. Certbot successfully received and deployed the certificate to the Nginx configuration, enabling HTTPS for both domain names. The certificate is stored under /etc/letsencrypt/live/prewebsite.online/, with the certificate expiring on 11 November 2026. Certbot also configured automatic certificate renewal, ensuring that the HTTPS certificate can be renewed automatically before it expires.

<img width="554" height="196" alt="image" src="https://github.com/user-attachments/assets/c088a0c5-42d7-4081-8497-6306e8c4c120" />

Next step was to use sudo systemctl status snapd to test if snapd is running

<img width="554" height="461" alt="image" src="https://github.com/user-attachments/assets/ef9ffea4-b290-4e34-8881-bfa097532f31" />

I verified the SSL/TLS certificate configuration using Certbot on the Nginx load balancer. The sudo certbot certificates command confirmed that a valid ECDSA certificate exists for both prewebsite.online and www.prewebsite.online, with an expiry date of 11 November 2026. I then tested HTTPS connectivity using curl -I https://prewebsite.online, which returned HTTP/1.1 200 OK, confirming that the domain is successfully accessible over HTTPS through Nginx. Finally, I used sudo certbot renew --dry-run to simulate the certificate renewal process. The test completed successfully and confirmed that the certificate can be renewed automatically without errors. This verified that HTTPS, certificate deployment, and automatic certificate renewal are all functioning correctly.

<img width="554" height="128" alt="image" src="https://github.com/user-attachments/assets/92d44232-6681-4ca4-b39a-640a11849e01" />

I verified that Certbot has an automatic renewal schedule configured on the Nginx load balancer. The command systemctl list-timers | grep certbot confirmed that certbot.timer is scheduled to run the Certbot service. I then checked the timer using sudo systemctl status certbot.timer, which showed that the timer is enabled and active (waiting) and is configured to run Certbot twice daily. The timer's next scheduled execution was also displayed, confirming that the system is ready to automatically check and renew the SSL/TLS certificate when necessary. This ensures that the HTTPS certificate for prewebsite.online can remain valid without requiring manual renewal.

<img width="436" height="390" alt="image" src="https://github.com/user-attachments/assets/a4d0a9d2-cc36-459e-955a-a2d0777ef860" />

As the final step of the project, I secured the website by enabling HTTPS using an SSL/TLS certificate obtained through Certbot.


