### SSH Keys
`ssh-keygen` will generate id_rsa and id_rsa.pub on linux or windows.  Put both files in the /keys directory on the docker-compose host before running `docker compose up`.  The public key will be added to the authorized_keys file in the host node image, and the private key will be added to the control node image. 

### Setting up
1) Ensure the keys are in the /keys directory on the docker-compose host.
2) Run `docker compose up` to start the containers.
3) Connect to the control node with `docker attach ansible-playground-control-node-1`
or ssh to the control node with user: `ansible` and password: `ansible`
4) Check the connection to the host containers from the control node with `ansible -m ping all'

### Notes
- You may need to connect to each host manually and accept the fingerprint before running ansible commands. `ssh root@host1` etc from the control node.

### To Do
- Enable ssh service on the control node container.
- Fix volume on the host node to make known_hosts persistent.
