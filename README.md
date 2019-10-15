```
Docker Build/ Run SMTP (for use by Jenkins Master):

# Clone
git clone https://github.com/RaderSolutions/docker-o365-smtp-relay.git
cd docker-o365-smtp-relay/

# Build docker container
docker build -t o365-smtp-relay .

# Start docker container (--detach to run in background) 
docker run --detach -i -t --restart unless-stopped \
	-p 25:25 \
	-e SYSTEM_TIMEZONE="America/Chicago" \
	-e MYNETWORKS="10.0.0.0/8 192.168.0.0/16 172.16.0.0/12" \
	-e EMAIL="user@domain.com" \
	-e EMAILPASS="the-password" \
	--name o365-smtp-relay \
	o365-smtp-relay

# To test
sendemail -f jim@bbc.com -t jim@bbc.com -u subject -m "RelayedViaOffice365" -s localhost:25 -o tls=no

# Stop (and remove otherwise the name is help on to)
docker stop smtp-relay && docker rm smtp-relay
```
