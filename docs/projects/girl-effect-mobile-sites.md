# Girl Effect mobile sites

We run mobile-optimised websites for Girl Effect which publish
information for adolescent girls. These sites are branded
in 3 different ways but are all based on the `molo-gem` codebase.

## Deployment

Developers are responsible for deploying their own changes.

In Spinnaker, check the `prod-deploy` pipeline to see the most
recent tag that has been deployed.

In Docker Hub, you can see the [list of molo-gem tags][dockerhub-tags].
Take the next tag after the one that is deployed.

[dockerhub-tags]: https://hub.docker.com/r/praekeltfoundation/molo-gem/tags/

Use the GitHub compare view to see the changes by making a URL like this:

```
https://github.com/praekelt/molo-gem/compare/dda4014...28ae1d8
```

In general, the person who has contributed the most to the diff is the person
who is responsible for deploying the change. This isn't an absolute rule
though, in case the person is away or unable to deploy.

This requires us to follow a principle that each merge to develop must
be self-contained.

Sometimes bugs will be discovered in QA (after a change is merged but
before it's deployed). In this case, avoid merging changes until the bug
is fixed and the entire feature can be deployed.

## Types of site

### Springster

Springster is the largest brand. It's available in 65 low and middle income
countries through [Facebook's Free Basics platform][freebasics].

[freebasics]: https://developers.facebook.com/docs/internet-org

### Ni Nyampinga

Ni Nyampinga is the Rwandan brand.

### Zathu

Zathu is the Malawi brand.
