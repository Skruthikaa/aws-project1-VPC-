# aws-project1-VPC-
1.create vpc with max range 10.0.0.0/16

<img width="1919" height="803" alt="Screenshot 2026-01-30 120540" src="https://github.com/user-attachments/assets/414840a6-640a-477e-b2c0-9dbee5680771" />
<img width="1919" height="797" alt="Screenshot 2026-01-30 120554" src="https://github.com/user-attachments/assets/eee58d4b-38b2-4036-809a-555b2e940d48" />

2. create internet gateway and attach to VPC

<img width="1919" height="672" alt="Screenshot 2026-01-30 120653" src="https://github.com/user-attachments/assets/55f06dc9-1a1d-4a8c-8763-852fd2ad28e9" />
<img width="1919" height="710" alt="Screenshot 2026-01-30 120742" src="https://github.com/user-attachments/assets/ce22ec56-e96b-4bd9-a3d7-d2cd5f049cb1" />
<img width="1914" height="716" alt="Screenshot 2026-01-30 120758" src="https://github.com/user-attachments/assets/19202879-5832-4bd3-b06c-60392e6f40e2" />

3. create 6 subnets according to the below info
You must create exactly 6 subnets, each with different IP capacities.
Subnet Allocation Table
Subnet Name	Purpose	Required IPs	CIDR	Address Range
Shared	Large Internal Services	~8,192	/19	10.0.0.0 – 10.0.31.255
Platform	Containers / Tools	~4,096	/20	10.0.32.0 – 10.0.47.255
App	Application Tier	~2,048	/21	10.0.48.0 – 10.0.55.255
Web	Web Tier	~1,024	/22	10.0.56.0 – 10.0.59.255
Edge	Ingress / Load Balancers	~512	/23	10.0.60.0 – 10.0.61.255
Admin	Bastion / Ops	~256	/24	10.0.62.0 – 10.0.62.255

<img width="1919" height="804" alt="Screenshot 2026-01-30 121122" src="https://github.com/user-attachments/assets/22978a49-a9da-47fd-b806-16060331b04e" />
<img width="1919" height="538" alt="Screenshot 2026-01-30 121158" src="https://github.com/user-attachments/assets/ec50145c-4272-46f5-860a-03e37aab91e7" />

<img width="1919" height="786" alt="Screenshot 2026-01-30 121253" src="https://github.com/user-attachments/assets/f4c06a88-a35b-41db-b519-3e57b16d4f4b" />
<img width="1919" height="787" alt="Screenshot 2026-01-30 121420" src="https://github.com/user-attachments/assets/df4339ed-ccae-4f7d-979e-13d227b6a3fd" />
<img width="1919" height="803" alt="Screenshot 2026-01-30 121702" src="https://github.com/user-attachments/assets/7257bc06-6f1b-4c7c-a405-f976df293b80" />
<img width="1893" height="774" alt="Screenshot 2026-01-30 121803" src="https://github.com/user-attachments/assets/63cf6e68-22f6-4c45-8012-da505c58746a" />
<img width="1863" height="802" alt="Screenshot 2026-01-30 121926" src="https://github.com/user-attachments/assets/228b6696-68a1-441d-893a-9a4b73926960" />

<img width="1919" height="720" alt="Screenshot 2026-01-30 121954" src="https://github.com/user-attachments/assets/44bbff12-7304-4f3a-bdfe-3f1eebfb4164" />

4.now create public route table and private route table 

<img width="1919" height="781" alt="Screenshot 2026-01-30 122306" src="https://github.com/user-attachments/assets/88d2c23a-e5f0-4bef-a3d1-5d60735e3a6e" />
<img width="1919" height="740" alt="Screenshot 2026-01-30 122342" src="https://github.com/user-attachments/assets/b6558cc5-e4fb-44d2-ad1e-1a3367925c8c" />

and attch the subnet according to the given info and route to the internet gateway
Subnet	Route Table
Admin	Public‑RT
Edge	Public‑RT

<img width="1919" height="773" alt="Screenshot 2026-01-30 122705" src="https://github.com/user-attachments/assets/f25ab63d-0ee6-432f-997e-74681d706493" />
<img width="1919" height="529" alt="Screenshot 2026-01-30 122818" src="https://github.com/user-attachments/assets/b249ff72-8860-43b6-9b97-7a36cfea4a34" />


Web	Private‑RT
App	Private‑RT
Platform	Private‑RT
Shared	Private‑RT

<img width="1919" height="793" alt="Screenshot 2026-01-30 122918" src="https://github.com/user-attachments/assets/4e1084cc-5c87-41ea-99ee-5b7709307cb2" />


5. Now check the network connection by creating ec2
6. now create ec2 by using pub subnet and one id pvt subnet

<img width="1919" height="781" alt="Screenshot 2026-01-30 123717" src="https://github.com/user-attachments/assets/64a8c7b1-49d5-4c01-ae04-82de027cc7b9" />
<img width="1918" height="714" alt="Screenshot 2026-01-30 123758" src="https://github.com/user-attachments/assets/dd9f823d-62af-4ea0-b486-972c2d22b98f" />

<img width="1919" height="785" alt="Screenshot 2026-01-30 123836" src="https://github.com/user-attachments/assets/eac3a5f8-2b3f-49f8-8df4-8fa85e36b588" />

6.now check the connection

<img width="1919" height="790" alt="Screenshot 2026-01-30 124110" src="https://github.com/user-attachments/assets/f0d98c43-4bb8-4ef1-aa39-8e7a6cd8b071" />

<img width="1916" height="866" alt="Screenshot 2026-01-30 124250" src="https://github.com/user-attachments/assets/5c04d9fb-9b2d-43db-81f3-c5f1fa698e82" />


