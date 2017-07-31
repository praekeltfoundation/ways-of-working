# Python packages

A lot of our code is published as Python packages on [PyPI][].

[PyPI]: https://pypi.org/

## Development

Make changes to the repository that contains the Python package using
the normal GitHub flow.

Bump the version in the repository. You might have to look in:

- `setup.py`
- `package/__init__.py`
- `docs/conf.py`

Push a new release tag to GitHub:

```
git tag 1.2.3
git push origin 1.2.3
```

## Release

The `.travis.yml` file will deploy the package to PyPI as the
[`praekelt.org` user](https://pypi.org/user/praekelt.org/).

For each package repository, there's another repo prefixed with `docker-`. For
example, `junebug` and `docker-junebug`.

[pyup.io](https://pyup.io/) will make an automatic pull request to the `docker-` repo
to increment the `requirements.txt` file.

When that pull request is merged, Travis will build a container image and deploy
it to Docker Hub as the
[`praekeltorgdeploy` user](https://hub.docker.com/u/praekeltorgdeploy/)
to the
[`praekeltfoundation` namespace](https://hub.docker.com/u/praekeltfoundation/).

## Deployment

Use Mission Control to deploy the Docker Hub image to QA and production.
