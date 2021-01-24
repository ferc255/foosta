# Setting up React UI

## First launch
**If the directory with the application has already been created, skip this step.**

Install latest `Nodejs`. There are some problems installing react with an outdated version of nodejs - that's why you need the latest one. You are better to choose LTS (Recommended For Most Users).

Go to `https://nodejs.org` and check out the number of the LTS version. For example, if you see `14.15.4 LTS` on the main page of the website, it means you need to install 14th version.

The installation consists of two steps. The first one is to run a preparation script:
```bash
    curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
```

At the end of the script execution, you will see something similar to:
```
## Run `sudo apt-get install -y nodejs` to install Node.js 14.x and npm
## You may also need development tools to build native addons:
     sudo apt-get install gcc g++ make
## To install the Yarn package manager, run:
     curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
     echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
     sudo apt-get update && sudo apt-get install yarn
```

It's a good instruction. Indeed, it's pretty difficult to launch react app without `yarn` (a lof of errors occur).
The first command to build native addons isn't needed. You just need to install `nodejs` itself and `yarn`.

Nodejs:
```bash
    sudo apt update && sudo apt install nodejs -y
```
Yarn:
```bash
    curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
    sudo apt update && sudo apt install yarn -y
```

Now you can initialize react app:
```bash
    npx create-react-app foosta_react
```

Verify that it works by typing:
```bash
    cd foosta_react
    npm start
```
and checking out `172.28.128.4:3000` in a browser.

After you do any changes, react automatically reloads a development server. The thing is the timestamp of the files is updated in vagrant not immediately - after you saved changes on the host, you have to do
```bash
    touch src/index.jsx
```
in a vagrant VM in order to see a fresh version of the website.

## Deploying an existing app.

TBD








Add this to /etc/nginx/nginx.conf

       server {
            listen 3003;

            location /api {
                  proxy_pass http://localhost:7070/;
            }

            location / {
                  proxy_pass http://localhost:3000/;
                  proxy_http_version 1.1;
                  proxy_set_header Upgrade $http_upgrade;
                  proxy_set_header Connection "Upgrade";
            }
        }

under `http` key.

And use 172.28.128.4:3000 as an entry point in the browser.