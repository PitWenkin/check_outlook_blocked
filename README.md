# Check Outlook Blocked
Nagios/Icinga script to check if the mail log file hints as to if Microsoft blocks emails

# Usage:
```
	 -l   logfile to analyse (default=/var/log/mail.log)
	 -W   number of times S3140 can appear in log before warning is returned (default=0)
	 -C   number of times S3140 can appear in log before critical is returned (default=1)
	 -w   number of times S3150 can appear in log before warning is returned (default=0)
	 -c   number of times S3150 can appear in log before critical is returned (default=1)
	 -s   number of times emails in direction of microsoft(*) can appear in log before waring is returned (default=0)
	 -S   number of times emails in direction of microsoft(*) can appear in log before critical is returned (default=0)
	 -h   Usage help
```

## Emails in direction of Microsoft

Are regarded as emails in direction of Microsoft those matching the regex:

`to=<[^>]*?@(hotmail|live|msn|outlook)\.(be|co.uk|com|com\.pt|de|es|fr|gr|ie|it|nl|pt)>`

which matches the following domains/tlds
```
hotmail.be
hotmail.co.uk
hotmail.com
hotmail.com.pt
hotmail.de
hotmail.es
hotmail.fr
hotmail.gr
hotmail.ie
hotmail.it
hotmail.nl
hotmail.pt
live.be
live.co.uk
live.com
live.com.pt
live.de
live.es
live.fr
live.gr
live.ie
live.it
live.nl
msn.pt
msn.be
msn.co.uk
msn.com
msn.com.pt
msn.de
msn.es
msn.fr
msn.gr
msn.ie
msn.it
msn.nl
msn.pt
outlook.be
outlook.co.uk
outlook.com
outlook.com.pt
outlook.de
outlook.es
outlook.fr
outlook.gr
outlook.ie
outlook.it
outlook.nl
outlook.pt
```

# Examples:

```
./check_outlook_blocked
OK - No trace of mail traffic to microsoft found in mailog! |S3140=0;0;1;; S3150=0;0;1;; SENT=0;0;0;;
```

```
./check_outlook_blocked -w 1 -C 5
OK - Found 50 mail(s) going to microsoft in mailog! |S3140=0;0;1;; S3150=0;1;5;; SENT=50;0;0;;
```

```
./check_outlook_blocked -s 10 -S 50
WARNING - Found 20 mail(s) going to microsoft in mailog! |S3140=0;0;1;; S3150=0;0;1;; SENT=20;10;50;;
```
