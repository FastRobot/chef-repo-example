# Example chef-repo for controlling policy via CI/CD processes

Use this as a starting point to manage all of the unversioned chef policy objects via source control.

The idea is that ALL policy flowing into your chef org comes through this repo, cookbooks are brought in via `berks install && berks upload` then Jenkins (or similar) runs `knife upload /` in a controlled fashion.

# Good enough for dev!

This should be a starting point to CI at least your development chef-repo. I would not attempt to use this in production until you'd found some reasonable tests to apply and proof prod against the mistakes I know are coming.

# Author
Lamont Lucas, lamont@fastrobot.com

PRs welcome, I'd love to extend this example to cover other CI systems.

