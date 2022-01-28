
1. A machine that is Docker-enabled 
2. An internet connection is required. 
3. A PC with 1 GB of free memory
4. Access to Google Drive
5. According to the [instrcutions](https://conf.researchr.org/track/icse-2022/icse-2022-artifact-evaluation), we built Docker Images using amd64 architecture. Therefore, If your Mac contains an Apple chip, as specified in the installation guide, the docker images may not operate as intended. This can be found under About your Mac -> Processor. If you use MacOS, you must have an Intel processor on your computer in order to execute the docker containers. 
6. We have created the Docker Images that has `amd64` architecture as per the [instrcutions](https://conf.researchr.org/track/icse-2022/icse-2022-artifact-evaluation). According to [Docker installation guide](https://docs.docker.com/desktop/mac/apple-silicon/), if you use a Mac computer and your Mac has an apple chip, the docker images created for `amd64` migh not work  on  apple chip as expected. You can check type of the chip in the `About your mac` -> `Processor`. Therefore, If you use MacOS, you must have an Intel processor on your computer in order to execute the docker containers. 
    > Even though we prefer Macs with Intel processors, you may still run Docker containers on Macs with Apple chips with caution. [This StackOverflow question](https://stackoverflow.com/questions/65612411/forcing-docker-to-use-linux-amd64-platform-by-default-on-macos) answers how to run `amd64` Docker images on a PC with an Apple chip (`arm64`). Below are the steps. 
    > 1. Please follow the installation instructions to install [Docker for Apple Chip](https://docs.docker.com/desktop/mac/apple-silicon/). 
    > 2. execute `export DOCKER_DEFAULT_PLATFORM=linux/amd64`.
