# Unifi-video to Matrix message bridge

Script for translating email messages generated by Unifi-video to
Matrix picture messages.

Intended to be run on an email server as a pipe transport script.

## Idea

On our hackerspace we have some Unifi surveillance cameras which send
email on motion. They send alerts by email which is pretty messy. This
script listens to incoming emails and tralates them to Matrix picture
messages.

Also, it suppresses sending messages if the alarm has been
disarmed. For that purpose we have an API endpoint where to check
arming status.

## Requirements

```sh
sudo apt install jq uuid-runtime curl mpack
```

## Configuration

Copy template as your configuration file and set URLs, room name, and
Matrix access token.

```sh
cp matrix.conf.example matrix.conf
$EDITOR matrix.conf
```

Add pipe transport to your email server configuration. See
[Exim documentation of pipe transport](https://www.exim.org/exim-html-current/doc/html/spec_html/ch-the_pipe_transport.html)
for example. It works with variety of email servers but the next one
is for Exim virtual domain configuration:

```
unifi-matrix : |/opt/unifi-matrix/unifi_parser
```

Ensure the script is executable and its configuration file is readable
by the mail user. For example in Debian and Exim, the user is
`Debian-exim`.

See your mail server documentation or make a little test script to
find out which user it is run by if you have any issues.
