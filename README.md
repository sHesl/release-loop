# release-loop
This repo was an attempt to discover the feasibility of repeatedly updating an existing release; determining if there were any unknown restrictions, limitations or issues with updating a single release, adding large quantities of individual files across many individual update operations.


## How does it achieve the infinite loop?
By using a Github PAT instead of a `GITHUB_TOKEN` inside the action, you can create a loop in which every execution of an action ends with a `git push`, triggering the action to run again immediately after; the usual checks in place to prevent these loops only seem to apply to the `GITHUB_TOKEN`. Check `.github/workflows/loop.yaml` and [this issue](https://github.community/t/workflow-infinite-loop/16547) for more details.


## Results
With over 10k individual files added into the release, I think it is safe to say that most projects can rely on Github Releases even if they are planning on distributing large quantities of files within a single release. Once the release reaches this scale, actions are more likely to flake due to timeouts/500s.  
