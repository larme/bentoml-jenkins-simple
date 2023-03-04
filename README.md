# Simple example integration between BentoML and Jenkins

notes:

- need to ignore `.env/` or `bentoml build` will hang. `.bentoignore` provided by this repository should be enough
- need to add jenkins user to docker group. `sudo usermod -a -G docker jenkins` then reboot.
