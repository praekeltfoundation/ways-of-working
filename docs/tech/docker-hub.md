# Adding a new repository to Docker Hub

- Set up your own account on <https://hub.docker.com/>
- Get an existing admin (normally SRE) to add you to the `praekeltfoundation` organisation
- Create a new repository under the organisation for your new image
- Add the `automation` team as a collaborator to your new repository with write access
- Use the `travis encrypt` command locally to encrypt the `praekeltorgdeploy` Docker Hub password (from 1Password) - for example, encrypt `REGISTRY_PASS=supersecretpassword`. NOTE: if you are using `travis-ci.ORG` this will suffice. If you are using `travis-ci.COM` you may need to use the `--pro` flag e.g. `travis encrypt --pro 'REGISTRY_PASS="secret"'`. Travis CI are switching open source projects over to travis-ci.com and new projects will use `.com`.
- Use the encrypted password environment variable to do `docker login` in your Travis file like this:

    ```
    echo -n $REGISTRY_PASS | docker login -u "$REGISTRY_USER" --password-stdin
    ```

- You can then push an image to Docker Hub using [`docker-ci-deploy`](https://pypi.org/project/docker-ci-deploy/):

    ```
    docker-ci-deploy --version $VERSION --version-latest $IMAGE_NAME
    ```
