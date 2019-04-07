
### `Intro`
Easyer way to "mine" on a server with no gui (haven't seen any difference in hash speed compared to a normal browser)

### `Docker`
Installing docker can be found [here](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

Run a=<ban_account> b=<threads> it works best with even numbers (2,4,6,8,...).
```
docker run -d --restart always -e "a=ban_3zi3ku5dqbdn1uzggcu9gggut1bojsa1a1jurdqnmcnohy94nu6bo3fo19cp" -e "b=4" anzerr/bananominer:latest
```
##### `Thread count`
You can find the number of core with "lscpu" in the output look for this
```
Thread(s) per core:    2
Core(s) per socket:    12
Socket(s):             4
```
In this example we got (4 * 12 * 2) give us 96 threads

##### `Build`
To build image from the git repo
```
git clone https://github.com/anzerr/banano.miner.git miner && \
	cd miner && \
	docker build -t anzerr/bananominer:$(node -e "console.log(require('./package.json').version)") -t anzerr/bananominer:latest .

docker push anzerr/bananominer:$(node -e "console.log(require('./package.json').version)")
docker push anzerr/bananominer:latest
```

### `Node`
Installing node can be found [here](https://nodejs.org/en/download/package-manager/)

The package.json is missing puppeteer to setup the project
```
git clone https://github.com/anzerr/banano.miner.git miner && \
	cd miner && \
	npm i --only=prod && \
	npm i --save puppeteer@1.8.0
```

To run the project
```
node index.js ban_3zi3ku5dqbdn1uzggcu9gggut1bojsa1a1jurdqnmcnohy94nu6bo3fo19cp 4
```

### `Output format`
when running you should see output every 5sec show hash state

event	| hash per sec 	| total hashes 	| estimate mined in a day
--- 	| --- 			| --- 			| ---
console | 28 			| 751 			| 157.248