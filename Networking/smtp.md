# Intro
Simple Mail Transfer Protocol
https://computer.howstuffworks.com/e-mail-messaging/email3.htm
https://www.afternerd.com/blog/smtp/

This protocol
- Verifies the sender
- Sends outgoing email
- Reply back if outgoing email cannot be delivered

Default port: 25

SMTP is not standalone, it needs POP/IMAP to receive the email.
POP (i.e. Post Office Protocol)
IMAP (i.e. Internet Message Access Protocol)

POP:  Server --> Client
IMAP: Server <-> Client

Sending an email, SMTP receiver available:
       SMTP handshake                relay email                  forward
Sender --------------> SMTP (sender) -----------> SMTP (receiver) -------> POP/IMAP --> Receiver Inbox

Sending an email, SMTP receiver NOT available:
Sender --------------> SMTP (sender) -----------> SMTP queue

# Commands

VRFY: confirm the names of valid users
EXPN: reveals the actual address of a user or mailing list
RCPT TO: 