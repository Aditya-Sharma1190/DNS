<h2>DNS : A-Record Exercise</h2>

Connect to DC VM and Client VM using RDP<br />
username : mydomain.com\adiadmin<br />
password : Cyberuser1234<br />


From Client VM , Ping mainframe(Arbitrary name)<br />

![image](https://github.com/user-attachments/assets/2aab1237-19a7-42d5-b277-ac9cedf0481a)

This would fail as DNS Cache for Client VM does not have a entry for mainframe 

![image](https://github.com/user-attachments/assets/50666a82-7787-4dd9-98c4-fe71930738bb)

To check we can run ipconfig /displaydns , to see if there is any A Record for mainframe present here <br />


Copy the output and paste it in a notepad , and ctrl + f to find a entry for mainframe , we will get no results 

![image](https://github.com/user-attachments/assets/9a21eec3-33a7-4894-88bc-d0bbefc43b40)

After validating that there is no entry for mainframe available in the it's cache , Clinet VM will then refer it's host file 
and there is no entry for mainframe there as well 

![image](https://github.com/user-attachments/assets/583f6ede-83a8-4920-9bf6-7959a74662fe)

![image](https://github.com/user-attachments/assets/c9093b7b-00d2-441b-99db-c23969e18f0a)

After checking it's cache and Host file , Client VM will refer to the local DNS Server (DC VM)<br />

In DC VM , under Windows Administrative Tools >> DNS

![image](https://github.com/user-attachments/assets/4414bf1e-c224-4f38-840f-bf59a5814166)

![image](https://github.com/user-attachments/assets/22c40835-9dcf-4a4c-8fff-cade3543f2a3)

There is no A Record entry for mainframe available , We can create a new entry for mainframe here by using Private IP for DC VM

![image](https://github.com/user-attachments/assets/1c33ec43-f919-4355-b482-637aa77e1e4e)


![image](https://github.com/user-attachments/assets/32850a2e-af61-432e-b6de-8230d22eefcf)

![image](https://github.com/user-attachments/assets/2d51fd2a-a144-493b-acac-696676a23a82)

![image](https://github.com/user-attachments/assets/640a6f1f-bf0a-43f7-a46f-de978eac4fa8)

From Client VM , We can now ping mainframe .

![image](https://github.com/user-attachments/assets/ac7a6650-ef24-42e3-a55a-3ab36110ca38)

<h2>DNS : Local DNS Cache Exercise</h2>

In DC VM , If we change the IP for mainframe in DNS Manager >> Forward Look Up Zones<br />

From 10.0.0.4 to 8.8.8.8

![image](https://github.com/user-attachments/assets/0107d957-a366-4d76-a1d8-2b40623a0e41)

Next, From Client VM if we ping mainframe it will still ping 10.0.0.4, As the local DNS Cache has not been updated.

![image](https://github.com/user-attachments/assets/babdea99-85ad-4c3b-9b81-ec7c24d95396)

We can clear the cache by running ipconfig /flushdns 

![image](https://github.com/user-attachments/assets/8482cc4e-f206-45bd-aa06-eb02382de000)

If we ping mainframe now from Client VM , It will Ping 8.8.8.8

![image](https://github.com/user-attachments/assets/068a79b7-f471-4b46-a883-c8ba661b67e3)

<h2>DNS : CNAME Record Exercise</h2>

CNAME Records are used to map one name to another <br />
A Records map a  Host to IP<br />

In DC VM , under Windows Administrative Tools >> DNS >> Forward Lookup Zones >> mydomain.com >> New Alias CNAME

![image](https://github.com/user-attachments/assets/064e75b9-107a-4567-9b7d-9f979a5a2338)

![image](https://github.com/user-attachments/assets/ef93b9bc-0b7a-4eba-a38c-e7d2abcb17d3)

From Client VM , We can now ping Cat

![image](https://github.com/user-attachments/assets/69f32130-f463-4342-9898-acd29de18ebf)

![image](https://github.com/user-attachments/assets/786df63d-ec03-4f88-b411-ba2e94da21ee)
























