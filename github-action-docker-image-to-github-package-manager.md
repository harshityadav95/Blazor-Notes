# Github Action : Docker Image to Github Package Manager

```text
# This file wont do us much good in this location, make sure you change the path as directed to continue!

name: Docker CD

on:
  push:
    paths:
      - "**Dockerfile**"
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v1
      - name: npm install and build webpack
        run: |
          npm install
          npm run build
      - uses: actions/upload-artifact@master
        with:
          name: webpack artifacts
          path: public/
  test:
    runs-on: ubuntu-latest
    needs: build
    strategy:
      matrix:
        os: [ubuntu-lastest, windows-2016]
        node-version: [12.x, 14.x]

    steps:
      - uses: actions/checkout@v1
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}
      - uses: actions/download-artifact@master
        with:
          name: webpack artifacts
          path: public
      - name: npm install, and test
        run: |
          npm install
          npm test
        env:
          CI: true
  Build-and-Push-Docker-Image:
    runs-on: ubuntu-latest
    needs: test
    name: Docker Build, Tag, Push

    steps:
    - name: Checkout
      uses: actions/checkout@v1
    - name: Download built artifact
      uses: actions/download-artifact@master
      with:
        name: webpack artifacts
        path: public
    - name: Build container image
      uses: docker/build-push-action@v1
      with:
        username: ${{github.actor}}
        password: ${{secrets.GITHUB_TOKEN}}
        registry: docker.pkg.github.com
        repository: harshityadav95/github-actions-for-packages/tic-tac-toe
        tag_with_sha: true
```



**Before we can use this Docker image, you will need to generate a** [**personal access token**](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line) **that contains the following permissions:**

* repo \(all\)
* write:packages
* read:packages

We will use this token to log in to Docker, and authenticate with the package.

### Step 6: Run your Docker Image

#### :keyboard: Activity: Run your image locally

1. Find your image information by typing `Docker image ls`

   ```text
    ![screenshot of output from Docker image ls command: lists docker images, REPOSITORY TAG and docker URL](https://i.imgur.com/UAwRXiq.png)
   ```

2. Use the following command to run a container from your image:

   ```text
        docker run -d -it --rm -p 8080:80 --name ttt <YOUR_IMAGE_NAME:TAG>
   ```

3. Replace `YOUR_IMAGE_NAME` with your image name under the `REPOSITORY` column
4. Replace `TAG` with the image tag under the `TAG` column

   ```text
    ![example of running the docker command listed above](https://i.imgur.com/hr6N9nk.png)
   ```

5. Press **Enter**

If everything went well, you will see hash value as output on your screen.

#### ![keyboard](https://github.githubassets.com/images/icons/emoji/unicode/2328.png) Activity: Log in to Docker

1. Open your terminal \(Bash or Git Bash recommended\)
2. Use the following command to log in:

   ```text
   docker login docker.pkg.github.com -u USERNAME -p TOKEN
   ```

3. Replace `USERNAME` with your GitHub username
4. Replace `TOKEN` with the Personal Access Token you just created
5. Press **Enter**

If everything went well, ![crossed\_fingers](https://github.githubassets.com/images/icons/emoji/unicode/1f91e.png) you should see `Login Succeeded` in your terminal.

### Step 5: Pull your image

#### :keyboard: Pull the image from GitHub Packages to your local environment

1. Copy and paste the `pull` command from the package instructions into your terminal. It should look something like this:
   * `docker pull docker.pkg.github.com/harshityadav95/js-build/tic-tac-toe:f29`

     ![screenshot of the pull command on the GitHub package page](https://i.imgur.com/pFQgfSZ.png)
2. Press **Enter**

You should see output indicating that the pull was successful, like `Status: Downloaded newer image for docker.`

![screenshot of successful Docker image output](https://i.imgur.com/i07kF2J.png)

