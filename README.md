# Dev Ops Setup  

## Description  
The Dev Ops Env Setup repository is consists of a docker compose file required to spin up build tools commonly used in a Dev Ops pipeline. The repository can be used for testing automation scripts.


## Tools spun up 
    1. Teamcity Server (http://localhost:8111)
    2. Teamcity Agent (http://localhost:9090)
    3. Postgres (localhost:5432)
    4. Redis
    5. Gitlab (http://localhost:30080 && ssh://localhost:3022)

## Network
The tools are all spun up on the devops network. Within the network, the tools have the following hostnames/exposed ports:

| Tool            | hostname       | ports |  
|-----------------|----------------|-------|  
| Teamcity Server | teamcityserver | 8111  |  
| Teamcity Agent  | teamcityagent  | 9090  |  
| Postgres        | devopsdb       | 5432  |  
| Redis           | devopsredis    | N/A   |  
| GitLab          | devopsgitlab   | 30080, 30022|

## Setup
To begin using the Dev Ops Env, first begin by pulling down the docker dependencies:  
NOTE: The GitLab application may take a few minutes to start up
```bash
git clone https://github.com/tomd8451/dev-ops-env.git
cd dev-ops-env
docker-compose up -d
```

#### TeamCity Server Setup
1)  To begin setting up TeamCity, navigate to [http://localhost:8111](http://localhost:8111) to begin setting up Teamcity.
![NavigateToTCScreenshot](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/01_NavigateToTeamcity.png?raw=true)  

2)  When prompted, select PostgreSQL and click to refresh JDBC drivers
![SelectPostgreSQL](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/02_SelectPostgreSQL.png?raw=true)  

3)  Enter the following credentials to connect TeamCity Server to your running PostgreSQL container:  

    | Field                | Value    |  
    |----------------------|----------|  
    | Database host[:port] | devopsdb |  
    | Database Name        | teamcity |  
    | User Name            | teamcity |  
    | Password             | teamcity |  
    
    ![EnterDBCreds](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/03_EnterDBCreds.png?raw=true)  

4)  Then create the credentials for the Teamcity Admin account.  
![TeamcityAdminCreds](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/04_CreateTCAdminCreds.png?raw=true)  

5)  Now that the server is running, navigate to the Agents tab to connect the running build agent.
![NavigateToAgents](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/05_NavigateToAgents.png?raw=true)  

6)  Select the Unauthorized Agents tab to view the dockerized build agent.
![ViewUnauthorized](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/06_ViewUnauthorizedAgents.png?raw=true)  

7)  Click the unauthorized hyperlink and authorize the build agent.
![AuthorizeBuildAgent](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/07_AuthorizeDockerizedBuildAgent.png?raw=true)  

8)  Select the Connected tab and verify your dockerized build agent is connected (this may take a few moments).  
![ViewUnauthorized](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/08_VerifyBuildAgentConnects.png?raw=true)  

#### Bitbucket Setup  
9)  Navigate to [http://localhost:7990](http://localhost:7990)
![NavigateToBitbucket](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/09_NavigateToBitBucket.png?raw=true)  

10)  Choose to get an evaluation license.
![BitbucketEval](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/10_ChooseToGetAnEvaulationLicense.png?raw=true) 

11)  Choose Bitbucket Server.
![BitbucketServer](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/11_ChooseBitbucketServerAndGenerateLicense.png?raw=true)  

12)  Confirm installing license to running server.
![ConfirmInstall](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/12_ConfirmInstallingLicenseToInstance.png?raw=true)  

13)  Click Next after license has been added.
![ClickNext](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/13_ClickNextAfterLicenseHasBeenAdded.png?raw=true)  

14)  Create Bitbucket Admin credentials.
![CreateAdminCreds](https://github.com/tomd8451/dev-ops-env/blob/bitbucket/docs/14_CreateBitbucketAdminCreds.png?raw=true)  