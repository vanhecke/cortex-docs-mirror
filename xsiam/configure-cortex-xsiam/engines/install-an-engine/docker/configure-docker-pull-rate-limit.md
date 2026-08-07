# Configure Docker pull rate limit

Docker enforces a [pull rate limit](https://www.docker.com/blog/scaling-docker-to-serve-millions-more-developers-network-egress/) on public images. The limit is based on an IP address or as a logged-in Docker hub user. The default limit (100 pulls per 6 hours) is usually high enough for Cortex XSIAM's use of Docker images, but the rate limit may be reached if using a single IP address for a large organization (behind a NAT). If the rate limit is reached, the following error message is issued:

`Error response from daemon: toomanyrequests: You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limit.`

To increase the limit:

1.  Sign up a free user [in the Docker hub](https://hub.docker.com/signup/).

    The pull limit is higher for a registered user (200 pulls per 6 hours).
2.  Authenticate the user on the engine machine by running the following command.

    **`sudo -u demisto docker login`**
3. (Optional) Instead of manually logging in to Docker to pull images, you can edit the [Docker config file](https://docs.docker.com/engine/reference/commandline/login/) to use credentials from the file or from a credential store.
