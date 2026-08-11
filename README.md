# load-balancer-with-nginx
A step-by-step DevOps guide to configuring Nginx as a Layer 7 load balancer on Ubuntu. Features local DNS mapping using /etc/hosts, upstream server pooling, and HTTP/HTTPS traffic distribution for scalable web infrastructure.

<img width="554" height="94" alt="image" src="https://github.com/user-attachments/assets/f1251ce5-8364-4dee-b8b2-671442f50960" />

My first step for this project was to create an instance named nginxlb. 

<img width="554" height="143" alt="image" src="https://github.com/user-attachments/assets/bf875496-65ed-4d2a-b621-b4cde990f85a" />

I edited inbound rules and opened port 80 to allow HTTP connections, and I opened port 443 to secure HTTPS connections.

<img width="554" height="30" alt="image" src="https://github.com/user-attachments/assets/846f0dd5-5f24-4726-8307-286bf3590fce" />

I had to restart web1 and web2 but in the process webs erver 2 could not start meaning I had to change instance type from t3micro to t3small

<img width="554" height="218" alt="image" src="https://github.com/user-attachments/assets/cbe3e54c-1cb3-4cad-b50f-3343abcf02ff" />



