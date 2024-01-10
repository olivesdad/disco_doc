# Discord Tool

The objective of this project is to create some rust projects that can do Discord things. I'm planning on creating 3 parts
    
1. **disco_hooker_service**: discord service that will run as a systemd service on a linux machine. It will utilize the [disco_hooker](https://github.com/anikiandy/disco_hooker) tool to send messages to discord webooks. This service should periodically check something for updates and send webhooks if there is an update maybe. It should also listen to some IPC socket that will allow updating up the webhook list via a cli tool. 
2. **discordcli**: Utilize discord bot api (crate currently undecided) to listen to some channels and print new messages to terminal
3. `discoctl` will be the cli tool that will send messages to the IPC socket to interact with the discord service and also the maybe the discord bot thing

## Plan of Execution
As this the primary objective of this project is learning rust for linux and probably NixOS. I want to thoroughly understand the concepts so I will be building smaller projects to practice the main components. 
- [ ] maybe setup ci to deploy this documentation as a github webpage
- [ ] Setup nix dev environment. This should just be a `shell.nix`
- [ ] Small project 1: Learn IPC Sockets
    - [ ] IPC1 : this will represent listener/service will just run a loop and listen to one side of the channel and print out strings sent from the sender tool. Also we should figure out how to send success/fail messages or signals to the cli
    - [ ] IP2 : This project will represent the discoctl program it will be executed with a string argument that it will just send to the IPC socket to the listener and it should probably wait or recieve a response that something happened and maybe timeout if the socket is poopy
        - [ ] use this to figure out arg parsing
- [ ] Create disco_hooker_service and discoctl in parallel
    - [ ] Use IPC1 as the base for disco hooker and get it to send hooks when it recieves anything
        - [ ] should utilize the load webhooks from json 
    - [ ] Use IPC2 as the base for `discoctl` just send strings
- [ ] Work on "advanced" features
    - [ ] Disco_hooker_service should impliment function to add a url to the webhook list
    - [ ] Disco_hooker_service should impliment functions to maybe update user name
    - [ ] Figure out a way to manage a config file json file. not sure which side should be responsible for this
- [ ] Work out logging what the disco_service is doing
- [ ] figure out how Nixify the service


