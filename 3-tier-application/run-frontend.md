## Run the application
### Move to frontend directory
```bash
~/ems-ops-phase-0/react-hooks-frontend$
```
### Install npm to start the frontend
```bash
sudo apt install npm
```
### Run the application
```bash
npm start
```
### Run the application in browser
> [http://localhost:3000](http://localhost:3000)
#### Output
##### Home
![image](https://github.com/user-attachments/assets/badbb7e4-3405-4a46-9724-7b249d9db447)
##### Add employee
![image (1)](https://github.com/user-attachments/assets/dc5ae649-7084-457d-b28b-10e2ddf2fb43)


## Error
### Err 1 : 
If any npm start occurs,
![image](https://github.com/user-attachments/assets/760c7c79-3f6f-4afa-aad3-64d641725890)
Use this following command,
```bash
export NODE_OPTIONS=--openssl-legacy-provider
npm start
```


