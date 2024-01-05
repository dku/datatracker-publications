# datatracker-publications
fetching a user's IETF documents from the datatracker

This project contains two tools for fetching and formatting metadata
for IETF documents (RFCs and Internet Drafts).

1. [tracker-doc](tracker-doc): for fetching document metadata by user-id (datatracker ID)
2. [bibdoc](bibdoc): for formatting document metadata in text or bibtex format

These are two Clojure scripts that are executed by
[Babashka](https://github.com/babashka/babashka) – a native Clojure
interpreter for scripting. Please see below for installation
instructions.


## Usage

### tracker-doc
Fetching document metadata by user-id (datatracker ID) from the IETF datatracker.

    Usage: tracker-docs <options> user-id
	
	Options
	--rfcs        get RFCs
    --active-ids  get active Internet Drafts
    --expired-ids get expired Internet Drafts
    --all-ids     get all Internet Drafts
    --all         get all RFCs and Internet Drafts (default)

Example:
``` bash
./tracker-doc --rfcs dirk.kutscher@neclab.eu 
rfc3259 rfc6920 rfc6920 rfc7069 rfc7778 rfc7927 rfc7927 rfc8763
```

Example:
``` bash
./tracker-doc --active-ids dirk.kutscher@neclab.eu 
draft-irtf-t2trg-iot-edge draft-li-icnrg-damc draft-oran-icnrg-reflexive-forwarding draft-irtf-coinrg-dir draft-fmbk-icnrg-metaverse
```

### bibdoc
Formatting document metadata in text or bibtex format.

    Usage: bibdoc <options> <docnames>
    
	Options
	--stdin       read document names from stdin instead of from argument list
	--bibtex      generate bibtex instead of text bibliographic entries
	
Example:
``` bash
./bibdoc rfc3259 draft-irtf-icnrg-pathsteering
Colin Perkins, Dirk Kutscher, Joerg Ott; A Message Bus for Local Coordination; RFC3259; October 2015; https://datatracker.ietf.org/doc/rfc3259/
Ilya Moiseenko, David R. Oran; Path Steering in CCNx and NDN; Internet Draft draft-irtf-icnrg-pathsteering (Work in Progress); December 2023; https://datatracker.ietf.org/doc/draft-irtf-icnrg-pathsteering/07/
```

Example:
``` bash
./bibdoc --bibtex rfc3259 draft-irtf-icnrg-pathsteering
@techreport{RFC3259,
  author = "Colin Perkins, Dirk Kutscher, Joerg Ott",
  title = "A Message Bus for Local Coordination",
  howpublished = "Internet Requests for Comments",
  type = "RFC",
  number = "3259",
  year = "2015",
  month = "October",
  issn = "2070-1721",
  publisher = "RFC Editor",
  institution = "RFC Editor",
}
@techreport{I-D.draft-irtf-icnrg-pathsteering,
  author = "Ilya Moiseenko, David R. Oran",
  title = "Path Steering in CCNx and NDN",
  howpublished = "Work In Progress",
  type = "Internet Draft",
  number = "draft-irtf-icnrg-pathsteering/07",
  howpublished = "\url{https://datatracker.ietf.org/doc/draft-irtf-icnrg-pathsteering/07/}",
  year = "2023",
  month = "December",
  institution = "IETF Secretariat",
}
```


Example:
``` bash
./tracker-doc --rfcs dirk.kutscher@neclab.eu | ./bibdoc --stdin
Colin Perkins, Dirk Kutscher, Joerg Ott; A Message Bus for Local Coordination; RFC3259; October 2015; https://datatracker.ietf.org/doc/rfc3259/
Stephen Farrell, Dirk Kutscher, Christian Dannewitz, Börje Ohlman, Ari Keränen, Phillip Hallam-Baker; Naming Things with Hashes; RFC6920; January 2020; https://datatracker.ietf.org/doc/rfc6920/
Stephen Farrell, Dirk Kutscher, Christian Dannewitz, Börje Ohlman, Ari Keränen, Phillip Hallam-Baker; Naming Things with Hashes; RFC6920; January 2020; https://datatracker.ietf.org/doc/rfc6920/
Richard Alimi, Akbar Rahman, Dirk Kutscher, Y. Richard Yang, Haibin Song, Kostas Pentikousis; DECoupled Application Data Enroute (DECADE); RFC7069; November 2013; https://datatracker.ietf.org/doc/rfc7069/
Dirk Kutscher, Faisal Mir, Rolf Winter, Suresh Krishnan, Ying Zhang, Carlos J. Bernardos; Mobile Communication Congestion Exposure Scenario; RFC7778; March 2016; https://datatracker.ietf.org/doc/rfc7778/
Dirk Kutscher, Suyong Eum, Kostas Pentikousis, Ioannis Psaras, Daniel Corujo, Damien Saucez, Thomas C. Schmidt, Matthias Wählisch; Information-Centric Networking (ICN) Research Challenges; RFC7927; December 2018; https://datatracker.ietf.org/doc/rfc7927/
Dirk Kutscher, Suyong Eum, Kostas Pentikousis, Ioannis Psaras, Daniel Corujo, Damien Saucez, Thomas C. Schmidt, Matthias Wählisch; Information-Centric Networking (ICN) Research Challenges; RFC7927; December 2018; https://datatracker.ietf.org/doc/rfc7927/
Akbar Rahman, Dirk Trossen, Dirk Kutscher, Ravi Ravindran; Deployment Considerations for Information-Centric Networking (ICN); RFC8763; April 2020; https://datatracker.ietf.org/doc/rfc8763/
```

## Dependencies

* [Babashka – native Clojure interpreter for scripting](https://github.com/babashka/babashka)

## TODO

* better error handling
* documentation
