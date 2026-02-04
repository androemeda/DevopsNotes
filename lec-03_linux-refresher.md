CI/CD → automate build, test and deploy so code can go to prod fast and safely  

CI = continuous integration  
CD = continuous delivery / continuous deployment  

CI starts when code is pushed to git repo  

Typical CI flow:
- linting → catch basic code issues early  
- build → download deps, compile / package  
- unit tests → test small units of code  
- mocking used in unit tests when functions depend on other functions or APIs  
- SAST → scan source code for security issues  
- SCA → check open-source libraries for known vulnerabilities  

Artifacts:
- output of CI pipeline  
- examples: jar, war, exe, docker image  
- same artifact is promoted across environments  

Docker:
- docker image = static artifact  
- built layer by layer on top of base image  
- layers are cached → faster builds  
- images are pushed to artifact repository  

CD:
- starts from artifact repo  
- deploys artifact to environments  

SIT (system integration testing):
- first environment where full system is deployed  
- checks interaction between modules / services  
- not isolated like unit tests  

Continuous delivery:
- deployment automated till staging / pre-prod  
- production deploy usually needs manual approval  

Continuous deployment:
- every successful pipeline auto-deploys to prod  
- no manual approval, very fast releases  

Security & testing in CD:
- integration testing  
- performance testing  
- DAST → security testing on running application  

Linux:
- UNIX came first → Linux inspired from it  
- Linux is open source and used heavily on servers  
- kernel manages CPU, memory, storage, I/O, security  

Kernel types:
- monolithic kernel  
- microkernel  

Linux basics:
- shell (bash/zsh) for command line  
- file system under `/`  
- process and user management  

AWS IPs:
- private IP → internal VPC communication  
- public IP → changes on stop/start  
- elastic IP → static, used for production endpoints  
