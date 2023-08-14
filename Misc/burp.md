# Tabs
## Proxy
What allows us to funnel traffic through Burp Suite for further analysis

## Target
How we set the scope of our project. We can also use this to effectively create a site map of the application we are testing.

## Intruder
Incredibly powerful tool for everything from field fuzzing to credential stuffing and more

### Attack types
Wordlist1:
Admin
Root

Wordlist2:
azerty
1234
the_true_password

Payload:
/socket.io/?USER=§user§&PASSWORD=§pwd§

#### Sniper
Provide Wordlist1

/socket.io/?USER=Admin&PASSWORD=pwd
/socket.io/?USER=user&PASSWORD=Admin
/socket.io/?USER=Root&PASSWORD=pwd
/socket.io/?USER=user&PASSWORD=Root

#### Battering Ram
Provide Wordlist1

/socket.io/?USER=Admin&PASSWORD=Admin
/socket.io/?USER=Root&PASSWORD=Root

#### Pitchfork
Provide Wordlist1
Provide Wordlist2

/socket.io/?USER=Admin&PASSWORD=azerty
/socket.io/?USER=Root&PASSWORD=1234
-> Stops because no more elements in Wordlist1

#### Cluster Bomb
Provide Wordlist1
Provide Wordlist2

/socket.io/?USER=Admin&PASSWORD=azerty
/socket.io/?USER=Admin&PASSWORD=1234
/socket.io/?USER=Admin&PASSWORD=the_true_password
/socket.io/?USER=Root&PASSWORD=azerty
/socket.io/?USER=Root&PASSWORD=1234
/socket.io/?USER=Root&PASSWORD=the_true_password

## Repeater
Allows us to 'repeat' requests that have previously been made with or without modification. Often used in a precursor step to fuzzing with the aforementioned Intruder

## Sequencer
Analyzes the 'randomness' present in parts of the web app which are intended to be unpredictable. This is commonly used for testing session cookies

## Decoder
Tool that allows us to perform various transforms on pieces of data. These transforms vary from decoding/encoding to various bases or URL encoding.
![](burp/burp0.png)

## Comparer
Tool we can use to compare different responses or other pieces of data such as site maps or proxy histories (awesome for access control issue testing). This is very similar to the Linux tool diff.

## Extender
Similar to adding mods to a game like Minecraft, Extender allows us to add components such as tool integrations, additional scan definitions, and more!

This will require Jython, under Options
https://www.jython.org/download.html

## Scanner
Automated web vulnerability scanner that can highlight areas of the application for further manual investigation or possible exploitation with another section of Burp. This feature, while not in the community edition of Burp Suite, is still a key facet of performing a web application test.
