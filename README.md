# Challenge

## Infrastructure
### The whole infrastructure is configured in [docker-compose](./docker-compose.yml) file with following containers:
- blue_php : ports 9000, 9001
	- PHP 7
- blue_vue : port 8080
	- NodeJS v12
- blue_mysql : port 3306
	- MySQL v5.6
- blue_redis : port 6380
	- Redis 5
- blue_nginx : port 81
	- NGINX
- blue_network
	
## Notes
### For the project to run as expected the checklist below should be completed:
- [ ] The path organization demonstrated below is required
(I will send a zip from the project with the folders in place to make it easier,
but *docker, backend and frontend* are 3 isolated repositories in git):
	- root [docker](https://github.com/raphaelts3/bluecoding-docker)
		- back [backend](https://github.com/raphaelts3/bluecoding-back)
		- front [frontend](https://github.com/raphaelts3/bluecoding-front)
- [ ] All the ports mentioned in *Infrastructure* must be available
	- 9000
	- 9001
	- 8080
	- 3306
	- 6380
	- 81
	

## Installation
### The project has some installation scripts to help the process and must be executed in the following order:
```(project-root) $ chmod +x ./bin/install && ./bin/install```
- The line above should: 
	- Create the docker network
	- Prepare the dockers

```(project-root) $ chmod +x ./back/bin/install && cd back && ./bin/install && cd .. ```
- The line above should:
	- Copy .env.example to .env
	- Run composer install inside the php docker
	- Change ownership from /app/storage from php container to nginx one
	- Run migrate:rollback inside the php docker
	- Run migrate inside the docker
	- Run db:seed
	- Run gif:crawl 1 - This populates the db with some gifs
	- Run the unit tests
### At this point the vue instance should be down, but the following commands will prepare and run it again
```(project-root) $ chmod +x ./front/bin/install && ./front/bin/install```
- The line above should:
	- Install npm packages locally
	- Up the docker
	- Rebuild the npm packages inside the node docker
### At this point everything should be ready to use

## Implementation notes
- Endpoints from Backend
	- Postman documentation: https://documenter.getpostman.com/view/1749336/SWE3dzt4?version=latest#6c719a24-5bd1-4712-a44a-21c3469c10fb
	- The endpoints below doesn't require authentication:
		- /auth/login
		- /auth/register
		- /gifs
		- /g/{key}
	- All others require a Bearer Token that could be acquired on both /auth/login and /auth/register
- All endpoints documented are functional, however only /gifs and /gif/search are being consumed on Frontend yet
- The gifs are being crawled from the GIPHY free API, it could be a issue to the test, even though I put the same key I used on the .env.example


The system should be avaiable at: [http://127.0.0.1:8080]

- Account:
	- email: abc@abc.om
	- password: 123
