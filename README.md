# mvnw
custom maven wrapper to dynamically switch mirrors to internal repo if behind corporate netowrk, else use maven central (or other repositories described in pom.xml)

 Maven Wrapper is a maven-provided plugin, this isolates maven installation requirements and gives control to developers as to which maven they need to build their code with.

the mvnw we're using is also customized to work on VPN as well as over the internet by choosing relevant settings.xml based on the below 3 parameters:

- A. Is the build running on CICD tool in which case it'll use CICD default settings.xml controlled by devops
- B. Is INTERNAL.REPO reachable (set in mvnw script), it'll create a custom settings.xml to be used with internal repo.
- C. if not a  and b, fall back to default maven (for dependency resolution over the internet), this will honour default settings.xml set by user


Steps to use mvnw for the first time:
- copy .mvn and mvnw from repository.
- Initial run for mvnw may requires an active internet connection as it downloads the required maven from maven central and may not work without internet unless you've set up your internal repository for it.
- Run the below command to install the required dependencies 
  ```
  ./mvnw -version```


- Once mvnw has been run with active internet (without VPN). switch the network to office internet or VPN and run command 2.a again. this will setup the maven for vpn environment.
- You'll get below prompt when you first run over VPN:
```proxy settings not found
This is first time setting up nexus configuration.
Press any button to open settings.xml and update your user and password
```
- Press any key and it'll open new settings.xml, you'll have to update your OLM_ID and PASSWORD in the mentioned fields.

- Save and close the file, return to the terminal where you ran mvnw command and press any key to continue.
Your mvnw setup is completed!
