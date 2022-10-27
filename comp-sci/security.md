# TODO

## 参考

🔍 https://security.stackexchange.com/
🗣 Krebs, Ptacek https://latacora.micro.blog/archive/
🎗 Aumasson serious cryptography https://eli.thegreenplace.net/2019/summary-of-reading-october-december-2019/
🗄
* `system.md` application config
* `math.md` information theory

## current

## queue

* hacking cloud databases, CIDR, port scanning https://infosecwriteups.com/how-i-discovered-thousands-of-open-databases-on-aws-764729aa7f32#836b
* lab: VirtualBox for Windows on nix? https://nostarch.com/ethical-hacking
* https://www.cnn.com/2022/03/30/politics/ukraine-hack-russian-ransomware-gang/index.html
* https://github.blog/2022-02-22-github-advisory-database-now-open-to-community-contributions/ https://www.thoughtworks.com/radar/techniques?blipid=202203063
* reverse engineering
* https://thepythoncorner.com/posts/2021-08-30-how-to-create-virus-python/
* https://www.twilio.com/blog/security-metrics-count
* https://www.freecodecamp.org/learn/information-security/
* https://news.ycombinator.com/item?id=28979231
* tie mulitple emails to important accounts as disaster prevention https://news.ycombinator.com/item?id=28274880
* public key cryptography [MacCormick 4] https://austinvernon.eth.link/blog/pkexamples.html https://austinvernon.eth.link/blog/publickey.html

things to know https://www.netmeister.org/blog/infosec-competencies.html https://jacobian.org/2021/jul/8/appsec-pagnis https://latacora.github.io/careers/

roles https://www.netmeister.org/blog/infosec-skillsets.html
* _security engineering_: meta/mgmt 🗄 `google-sre-security.pdf` https://danielmiessler.com/study/ https://news.ycombinator.com/item?id=24031632
* _cryptography_: academics https://web.engr.oregonstate.edu/~rosulekm/crypto/
* _web_: knowing about SQL injection, XSS, CORS 🗄 `zalewski.pdf`
* _hacking_: Kali Linux, MetaSploit 🗄 `weidman-pen-testing.pdf` https://news.ycombinator.com/item?id=24718078
* _reverse engineering_: disassemblers/decompilers, C++, Windows 🗄 `python-grey-hat.pdf` https://www.begin.re/ https://nostarch.com/GhidraBook https://news.ycombinator.com/item?id=29084716 https://reverseengineering.stackexchange.com/ https://malwareunicorn.org/workshops/re101.html

* clean up https://cryptopals.com/ https://github.com/AntonKueltz/cryptopals https://www.hacker101.com/playlists/newcomers https://krebsonsecurity.com/2012/06/how-to-break-into-security-ptacek-edition/#more-15594 https://www.freecodecamp.org/learn/information-security/python-for-penetration-testing/ https://www.youtube.com/c/HackerSploit/playlists https://krebsonsecurity.com/2012/10/the-scrap-value-of-a-hacked-pc-revisited/ https://news.ycombinator.com/item?id=26071906 https://danielmiessler.com/blog/build-successful-infosec-career/ https://danielmiessler.com/study/information-security-definitions/
* https://sre.google/books/
* w/ Django https://www.youtube.com/watch?v=bvLJTNRpnt8
* ad blocking https://blog.codinghorror.com/an-exercise-program-for-the-fat-web/ https://news.ycombinator.com/item?id=23521399 https://blog.maskys.com/my-best-chrome-extensions/ https://hacker-tools.github.io/web/ https://hacker-tools.github.io/security/

## done

* _22_: switch to Brave
* _20_: second pass at auth
* _19_: first path at auth
* _17_: Networking for Dummies

# EXPLOITS

🛠 scan https://observatory.mozilla.org/ https://securityheaders.com/ https://snyk.io/

* _rootkit_: privilege escalation to root https://jvns.ca/blog/2013/10/08/day-6-i-wrote-a-rootkit/
* _remote code execution (RCE)_: getting access to someone's server and executing arbitrary commands https://news.ycombinator.com/item?id=23308945
* e.g. log4j https://github.com/Narasimha1997/py4jshell
* _zero-day_: attacker knows before owner knows
* _DoS (denial of service)_: designed to crash system vs. extracting data https://jacobian.org/2020/sep/11/analyzing-dos-vulnerabilities/ 

---

* _zero-knowledge proof (ZKP)_: someone prove that you know something without disclosing what you know https://www.notboring.co/p/zero-knowledge
* _command injection_: input causes system call on server
* _dictionary attack_: go through list of common passwords; form of brute force
* _directory traversal_: improper validation of user input leads to read access of directory (not the file itself; that’s LFI) --> http://www.example.com?file=../../etc/passwd
* _phishing_: elicit secrets via mimicry of legimate resource e.g. set up page to mimic company internal portal https://www.wsj.com/articles/the-teenager-behind-the-twitter-hack-and-how-he-did-it-11596563449
* _Spectre, Meltdown_: programs reading data from other programs, all the way down to kernel memory 
* _sim swap_: convince telco to assign number to new phone https://www.wsj.com/articles/the-teenager-behind-the-twitter-hack-and-how-he-did-it-11596563449
* _worm_: self-propagating sw [`tcp-ip-illustrated.pdf` 18.1]

* _packet sniffing_: if packets are sent in unencrypted fashion, can see session info
* _sensitive data_: https://github.com/hisxo/gitGraber https://github.com/trufflesecurity/trufflehog
* _tmi_: passwords in your repo, `debug!=true` in PROD https://github.com/6IX7ine/djangohunter
* _CSRF_: take login credentials and send to 3rd party site [Flask Web Dev 37] https://docs.djangoproject.com/en/2.1/ref/csrf/ https://www.fullstackpython.com/cross-site-request-forgery-csrf.html https://flask.palletsprojects.com/en/1.1.x/security/#cross-site-request-forgery-csrf https://testdriven.io/blog/csrf-flask/

## file inclusion

https://security.stackexchange.com/questions/174932/what-is-the-difference-between-local-file-inclusion-lfi-and-remote-file-inclus

* _local_: directory traversal + reading file
* _remote_: including file from remote source
* _how does it typically happen?_ improper validation of user input leads to the loading of an external resource into the server and execution therein
* _example_: http://www.example.com/vuln_page.php?file=http://www.hacker.com/backdoor
* `/etc/passwd`: how to read and [how to crack](https://pentestlab.blog/2012/07/23/dumping-and-cracking-unix-password-hashes/); actual passwords stored elsewhere in shadow password file [LPI 26]

## SQL injection

* https://jacobian.org/2020/may/15/preventing-sqli/ https://www.fullstackpython.com/sql-injection.html https://sqlwiki.netspi.com/ https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/ https://realpython.com/prevent-python-sql-injection/  https://www.djangoproject.com/weblog/2020/feb/03/security-releases/ https://blog.guilatrova.dev/how-sql-injection-attack-works-with-examples/
* _command injection_: passing malicious code to `os.system` or similar modules
* _prevention_: input validation, parameterized queries [as in Java PreparedStatement] vs. string concat so that input cannot affect the structure of the query
* _parameterized query_: sanitization
* _how do malicious queries get in?_ GET/POST parameters, cookie values, form fields
* _what happens when they get in?_ send script to browser—> browser executes —> logs keystrokes, takes session cookies, sends to own server

## XSS 

= 3rd-party JavaScript running on your site

* _how?_ submit form w/ malacious JS embedded in HTML attr https://flask.palletsprojects.com/en/1.1.x/security/#cross-site-scripting-xss https://24ways.org/2018/securing-your-site-like-its-1999/
* _why?_ read user cookies and send to 3rd party https://www.owasp.org/index.php/Cross-site_Scripting_(XSS) https://security.stackexchange.com/questions/36172/is-cookie-based-xss-exploitable
* _types_: stored vs. reflected https://shoptalkshow.com/episodes/250-web-security-april-king-alex-sexton/
* _sink_: https://tonybaloney.github.io/posts/xss-exploitation-in-django.html https://terjanq.github.io/Tiny-XSS-Payloads/index.html

__in action__

🔗 https://24ways.org/2018/securing-your-site-like-its-1999/

* couldn't submit `<script>`, but -> added attribute to html ala `<div style="background:url('javascript:alert(1)')">` 
> I don't understand two things about here: why URL executes (thought it only parsed file path to static resource) and why `javascript:` specifies a runtime (where else in CSS would this come up?)
* only worked on IE, but this was 2005
* couldn't invoke `document.body.innerHTML`, but -> can concatenate code and execute inside eval `eval('document.body.inne' + 'rHTML')`
* realized `innerHTML` contained links a few other user profiles
* realized he could hit MySpace API
* all recursion from there

# CRYPTOGRAPHY

🔍 https://crypto.stackexchange.com/
📚
* Erickson hacking (chapter 10)
* Sweigart ciphers

* real/academic cryptography is a math thing https://web.engr.oregonstate.edu/~rosulekm/crypto/
* diff btw cryptography and encryption https://security.stackexchange.com/questions/tagged/cryptography
* _opaque_: not human readable

elliptic curve cryptography
* https://paulmillr.com/posts/noble-secp256k1-fast-ecc/
* https://cryptobook.nakov.com/
* https://blog.cloudflare.com/a-relatively-easy-to-understand-primer-on-elliptic-curve-cryptography/
* https://fangpenlin.com/posts/2019/10/07/elliptic-curve-cryptography-explained/

---

* random number generator https://www.youtube.com/watch?v=nDv3yXdD0rk
* https://eli.thegreenplace.net/2019/the-chinese-remainder-theorem/
* RSA https://eli.thegreenplace.net/2019/rsa-theory-and-implementation/
* https://eli.thegreenplace.net/2019/diffie-hellman-key-exchange/
* https://news.ycombinator.com/item?id=24310842
* https://nostarch.com/seriouscrypto
* https://www.manning.com/books/real-world-cryptography
* https://nostarch.com/mangacrypto
* https://news.ycombinator.com/item?id=23384227 https://www.gkbrk.com/2020/03/encryption/ https://www.khanacademy.org/computing/computer-science/cryptography + 🗄 `cracking-codes.pdf` (owe Al Amazon review) https://missing.csail.mit.edu/2020/security/ https://www.manning.com/books/real-world-cryptography https://robertheaton.com/preventing-impossible-game-levels-using-cryptography/ https://www.cryptologie.net/article/496/whats-a-key-exchange/
* https://news.ycombinator.com/item?id=26560953
* digital signatures 📙 MacCormick ch. 9

## encryption

🗄
* `math.md` encoding
* `system.md` secrets

encryption https://danielmiessler.com/study/encoding-encryption-hashing-obfuscation/
* _code_: public protocol
* _cipher_: private protocol 📙 Sweigart ciphers 4
* how to crack 📙 Bhargava 11.217
* _encrypt_: text to code 📙 Sweigart 1.2 🗄`classic-compsci` https://robertheaton.com/2019/08/12/programming-projects-for-advanced-beginners-user-logins/ https://github.com/FiloSottile/age
* _decrypt_: code to text 📙 Sweigart 1.2
* _hash_: 🗄 `python.md`
* _nonce_: random number used in crypto to prevent replay attack https://en.wikipedia.org/wiki/Cryptographic_nonce#Authentication
* _obfuscate_: 

> anything that requires encryption requires a secret key https://stackoverflow.com/a/22463969
* breaking https://news.ycombinator.com/item?id=26085515
* AES-256 SHA256 https://hackernoon.com/very-basic-intro-to-aes-256-cipher-qxr32yk https://github.com/in3rsha/sha256-animation https://github.com/karpathy/cryptos https://sha256algorithm.com/ https://news.ycombinator.com/item?id=30244534 BYO SHA256 https://github.com/oconnor663/sha256_project https://github.com/francisrstokes/githublog/blob/main/2022/6/15/rolling-your-own-crypto-aes.md
* E4M (Paul Le Roux) was the basis for True Crypt https://news.ycombinator.com/item?id=11381625 Ptacek audited True Crypt https://news.ycombinator.com/item?id=9069295
* _PGP (Pretty Good Privacy)_: encryption for email; limited adoption https://latacora.micro.blog/2019/07/16/the-pgp-problem.html
* _Age_: https://github.com/FiloSottile/age https://www.youtube.com/watch?v=AAUJjwdCx4I 1:40
* _OTR_: https://robertheaton.com/otr1

symmetric
* sender encrypts using shared key, recipient decrypts using shared key
* _example_: Caesar cipher
* _advantages_: faster than asymmetric (file transmisssion/storage)
* _disadvantages_: how to transmit the key, key management (need different for each node in conversation and maybe even for each session)
* _sink_: https://dev.to/isaacandsuch/this-is-how-https-works-223d

asymmetric
* sender encrypts using public key, recipient decrypts using private key; aka PKI
* uses CA as passive (contra Kerberos) trusted third-party [`oreilly-ssh.pdf` 11.5.2]
* _analogy_: public key locks safe, private key opens it https://stratechery.com/2018/open-closed-and-privacy/
* _example_: Diffie-Helman, RSA [Bhargava 11.217-218] https://www.youtube.com/watch?v=AAUJjwdCx4I 2:10
* https://twitter.com/kosamari/status/838738015010848769
* _disadvantages_: key distribution i.e. if MitM swaps public key for theirs 📍link to image https://softwareengineeringdaily.com/2017/10/24/keybase-with-max-krohn https://www.youtube.com/watch?v=vsXMMT2CqqE
* _ECC_: like RSA but used in devices with less resources like smartphones

## hashing

🔗 https://github.com/HashPals/Name-That-Hash

* _hash_: output from hash function [Bhargava 11.214]
* _locality_: insensitive (slight diff in input changes hash completely) sensitive (slight diff in input changes hash only slightly) [Bhargava 11.216]
* _hash function_: https://austinvernon.eth.link/blog/hashexamples.html https://austinvernon.eth.link/blog/hash.html
* _rainbow table_: https://fasterthanli.me/articles/whats-in-a-rainbow-table

---

BYO https://www.reddit.com/r/learnprogramming/comments/33s79p/what_is_the_best_way_to_start_writing_my_own_hash/
hash function https://www.youtube.com/watch?v=cczlpiiu42M

* _hash function_: consistent i.e. input 'alice' always returns 42 [5.76] diff strings to diff nums i.e. input 'alice' returns 1 and input 'bob' returns 2 [Bhargava 5.76] https://wizardzines.com/comics/hash-functions/
```python
pass
```
* _one-way_: for identity comparison of sensitive data (does this input match a password?) salt = cannot convert hash back to input [Bhagava 11.215-218]

* _examples_: MD5 (vulnerable to collision attack, used for file integrity) SHA (use -256, not -1)
* _locality-sensitive_: for similarity comparison (are these two files similar?) magnitude of hash change reflects input string [Bhagava 11.216]
* _salt_: unique data added to one-way algo ❓ to differentiate it for everyone else using SHA-256 ❓ are one-way *really* one-way or does the addition of salt mean that it would take a ton of computing power and a million years to convert to unhash them?
* _checksum_: for identity comparison (are these two files the same?) [Bhagava 11.214] 📍 do tutorial of how Michael Kennedy uses checksums for caching https://pythonbytes.fm/episodes/show/21/python-has-a-new-star-framework-for-restful-apis @ 11:30
* _salt_: has function takes password and salt (random char) and outputs hash value, which is then stored instead of the naked user/pass; prevents dictionary attack (run through list of common user/pass) bc hacker could guess user/pass and hash func but not get value bc doesn't have salt
* _collisions_: n K to same V (which will be a linked list) [Bhagava 5.87]
* _load factor_: percentage of array indices occupied; 50% is good, above 100% and you're edging away from O(1) [Bhagava 5.90]
* _resize_: increase array size [Bhagava 5.91]
* _Merkle tree_: hash of hashes

# USERS

## auth

🗄 `application.md` security

vocab
* _authorization_: identity
* _authentication_: access
* aka permissions https://github.com/authzed/spicedb https://www.thoughtworks.com/radar/languages-and-frameworks?blipid=202203085
* _RBAC_: principle of least privilege
* role-based e.g. dba has full access to all fields to db but app dev will not see any personally identifiable info e.g. in Postgres can set permissions at the column level https://softwareengineeringdaily.com/2020/07/28/access-control-management-with-fouad-matin-and-dan-gillespie/

OAuth https://www.youtube.com/watch?v=xHFzhBjnMPI
* is now Okta? https://www.okta.com/okta-and-auth0/
* allow 3rd party to use data from service (e.g. Github) w/out exposing user creds from service to 3rd party https://stackoverflow.com/a/33704657
* authorization, not authentication e.g. 3rd party uses Github for OAuth to establish an identity for a new user https://stackoverflow.com/a/33704657
* OAuth2 simpler than OAuth1, which required non-standard client (couldn't curl) and had its own security layer (vs. HTTPS) https://brandur.org/accessible-apis
* framework, not protocol 🗄 `link.md`
* sometimes known as passwordless https://dzone.com/articles/how-passwordless-authentication-works
* _token types_: access token, id token https://auth0.com/blog/refresh-tokens-what-are-they-and-when-to-use-them/
* _components_: resource owner (user) client (app that user wants to use) server/provider (authenticates user, grants token to client, which I presume is then handed to user) https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2 https://stackoverflow.com/a/10282020
> When a user logs into our site with their Github account, we will redirect them to Github which then sends us a token that represents the user. https://learndjango.com/tutorials/django-allauth-tutorial

za
* _LDAP_: protocol to store/query directory of users/groups/perms; used for both authorization and authentication; services that use LDAP incl Active Directory and OpenLDAP https://news.ycombinator.com/item?id=23868081 https://news.ycombinator.com/item?id=32053961
```yaml
# https://www.youtube.com/watch?v=G6OhnMDU1J4
dn: CN=Alice, OU=sysadmin
# dn = distinguised name i.e. ID
# CN = common name i.e. human readable name
# OU = organization unit
```
* _Auth0_: sells platform built on OAuth https://stackoverflow.com/a/46782752
* _OpenID Connect_: newer version of OpenID that uses OAuth https://security.stackexchange.com/a/182083 https://security.stackexchange.com/a/130411 📍 https://www.youtube.com/watch?v=xHFzhBjnMPI https://stackoverflow.com/questions/1087031/whats-the-difference-between-openid-and-oauth
* _OpenID_: dead https://www.wired.com/2011/01/openid-the-webs-most-successful-failure/

Kerberos https://www.roguelynn.com/words/explain-like-im-5-kerberos/ https://web.mit.edu/kerberos/krb5-1.12/doc/index.html https://web.mit.edu/kerberos/www/dialogue.html
* single sign-on (SSO) for corporate networks https://stackoverflow.com/a/46188971
* authentication
* login: user/pass, user/keytab (secret but not a pw)
* _keytab_: db for keys https://web.mit.edu/kerberos/krb5-1.12/doc/basic/keytab_def.html
> or secret that's not a pw
* _components_: client, service you want to talk to, ticket granting server (TGS), key distribution center (KDC)
* _realm_: collection of services a client could potentially talk to
* uses symmetric encryption [`oreilly-ssh.pdf` 11.5.2]
* uses KDC as active trusted third-party, active insofar as each message has to go through KDC, unlike PKI in which client/server can talk to each other once certificate granted [`oreilly-ssh.pdf` 11.5.2]
* kinit

## cookies

📚 `gourley-http.pdf` chapter 11
🔗 https://tools.ietf.org/html/rfc7235 

* _cookie_: val set by server
```python
from http import cookies
c = cookies.SimpleCookie()
c['foo'] = 'foo val'
c.output()
'Set-Cookie: foo="foo val"'
```

auth flow https://security.stackexchange.com/q/87269
* req: form data to auth
* res: server generates session id -> uses session id to generate cookie for 'set-cookie' header -> res w/ 302
* req: browser redirects to new URL -> sends its new cookie value along
* res: server maps cookie to session id -> auths req

---

https://www.alexedwards.net/blog/working-with-cookies-in-go

🔗 https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies https://en.wikipedia.org/wiki/HTTP_cookie

authorization types https://testdriven.io/blog/flask-spa-auth/
* _session-based_: uses cookies
* _token-based_: uses localStorage

* HTTP basic auth https://blog.luisrei.com/articles/flaskrest.html https://www.youtube.com/watch?v=VW8qJxy4XcQ
* https://www.youtube.com/channel/UCnWO-PRzuPnPBg0KCg_RVPA https://developer.mozilla.org/en-US/docs/Web/HTTP https://hpbn.co/brief-history-of-http/
* HTTPS https://howhttps.works/ https://realpython.com/python-https/
* https://lchsk.com/stay-paranoid-and-trust-no-one-overview-of-common-security-vulnerabilities-in-web-applications.html https://24ways.org/2018/securing-your-site-like-its-1999/ https://hackernoon.com/10-common-security-gotchas-in-python-and-how-to-avoid-them-e19fbe265e03 https://kushaldas.in/posts/highest-used-python-code-in-the-pentesting-security-world.html https://www.freecodecamp.org/learn/information-security/information-security-projects/

diff btw cookie and token
* https://stackoverflow.com/q/17000835
* lots of people have this question https://stackoverflow.com/questions/1592534/what-is-token-based-authentication
* does user/pw on Django use cookies?
* token (identification) cookie (association); sites arent' after whether you are really you, just want to know associations around you (age, credit worthiness) in order to server ads?
* https://stackoverflow.com/a/38470665
* https://stackoverflow.com/a/50002308
* https://testdriven.io/blog/web-authentication-methods/
* https://www.youtube.com/watch?v=dinuA2KM3B4
* https://increment.com/apis/land-before-modern-apis/
* https://fly.io/blog/api-tokens-a-tedious-survey/ https://news.ycombinator.com/item?id=28295348
* cookies and sessions https://eli.thegreenplace.net/2011/06/24/django-sessions-part-i-cookies/
* email/pass https://learndjango.com/tutorials/django-log-in-email-not-username user/pass https://www.arp242.net/email-auth.html https://news.ycombinator.com/item?id=18767767 https://news.ycombinator.com/item?id=2861288

cookies https://tools.ietf.org/html/rfc2965
* _cookie_: opaque string sent to server for use as key to map to session https://eli.thegreenplace.net/2011/06/24/django-sessions-part-i-cookies/ https://stackoverflow.com/a/38470665
```js
// res
Set-Cookie: my_cookie_name=my_cookie_value
// req
Cookie: my_cookie_name=my_cookie_value
```
* can also store metadata (whether or not to remember your previous login) https://www.youtube.com/watch?v=QWw7Wd2gUJk 2:30
* view in browser via: dev tools > application > cookie https://www.youtube.com/watch?v=nfNrfi7HmLs
* https://news.ycombinator.com/item?id=25459530
* https://www.jefftk.com/p/why-i-work-on-ads
* _container_: separate cookies for different services (social, banking) https://hacker-tools.github.io/security/
* sessions 🗄 `system.md` caching

session
* collection of info re: instance of user interaction https://medium.com/@peterchang_82818/difference-session-cookie-token-vs-token-authentication-based-traditional-store-a177e8474ee3
* stored on server (typically via KV store like Redis bc non-volatile)
* _sticky_: each req from same user goes to same server (via load balancer)
* _fat URL_: URL incl user info [Gourley 11.5]

cookie types https://en.wikipedia.org/wiki/HTTP_cookie#Terminology
* _persistent_: login info
* _session_: date on this particular visit to site
* _3rd party_: tracking i.e. data brokerage

tracking w/ cookies
> Why does a website that orders food from restaurants need a Megabyte of javascript?6 I tried to figure that out by inspecting the API calls. It turned out they were tracking every mouse event. https://whatisjasongoldstein.com/writing/help-none-of-my-projects-want-to-be-spas/
* how it works: sent back to originator (e.g. FB) when 3rd party site include scripts (e.g. Like button, Google analytics) https://www.youtube.com/watch?v=QWw7Wd2gUJk 4:00
* _cookie policy_: list of other sites to whom cookies sent [ibid 5:00]
* regulation: ubiquitous GDPR banner to accept cookies
* block tracking cookies w/ extension (Privacy Badget, Ghostery) or browser (Brave, Safari)
* https://robertheaton.com/2017/11/20/how-does-online-tracking-actually-work/ https://robertheaton.com/2017/11/21/cookie-syncing-how-online-trackers-talk-about-you-behind-your-back/ https://robertheaton.com/2017/11/24/identity-graphs-how-online-trackers-follow-you-across-devices/ https://marvinblum.de/blog/server-side-tracking-without-cookies-in-go-OxdzmGZ1Bl

## passwords

🗄 `django.md` users

workflow https://robertheaton.com/2019/08/12/programming-projects-for-advanced-beginners-user-logins/
* how to validate registration: to prevent the waste of maintaining empty accounts https://testdriven.io/blog/sending-confirmation-emails-with-flask-rq-and-ses/ to prevent someone from accidentally reigstering wrong email and inadvertently giving someone access to their account [email - 'new feedback message']
* how to store: hash them https://cloud.google.com/blog/products/gcp/12-best-practices-for-user-account
* _change_: update for logged-in user
* _reset_: update for user who cannot login 📙 Osborn 1.10

---

* GPG https://www.youtube.com/watch?v=1vVIpIvboSg
* pwgen https://www.youtube.com/watch?v=G3aH2WYJxGA

password manager
* https://rutar.org/writing/some-tricks-with-unix-pass/
* https://rutar.org/writing/managing-secrets-from-the-command-line/

password protected files
* current: pw protection via Pages (on HD not pw-protected themselves) and plain text on pw-protected HD https://security.stackexchange.com/a/128495/160351
* pw-protection typically done via app like Pages or Excel https://security.stackexchange.com/q/62215/160351 vulnerable bc copy to system clipboard
* pw protection of plain text not possible bc OS will ignore, only possible to encrypt https://stackoverflow.com/questions/18525802/create-password-protected-text-file-using-java

* passwordless https://news.ycombinator.com/item?id=24830580 https://blog.google/technology/safety-security/a-simpler-and-safer-future-without-passwords
* https://news.ycombinator.com/item?id=26799021
* https://blog.codinghorror.com/youre-probably-storing-passwords-incorrectly/
* pasting https://news.ycombinator.com/item?id=23572023
* _cracking_: https://leahneukirchen.org/blog/archive/2019/10/ken-thompson-s-unix-password.html
* _manager_: Last Pass https://www.securityevaluators.com/casestudies/password-manager-hacking/ https://buttercup.pw/ https://medium.com/@stuartschechter/before-you-use-a-password-manager-9f5949ccf168 https://www.wsj.com/articles/why-you-should-consider-a-password-manager-1527645720?mod=article_inline https://www.mozilla.org/en-US/firefox/lockwise/ https://buttercup.pw/ https://changelog.com/podcast/325 https://hacker-tools.github.io/security/ https://lock.cmpxchg8b.com/passmgrs.html
* _QWERTY_
* _MFA/2FA_: people using Yubikey now https://threadreaderapp.com/thread/1140404696256937984.html https://apenwarr.ca/log/20190114 https://www.theverge.com/2017/7/10/15946642/two-factor-authentication-online-security-mess https://www.wsj.com/articles/the-security-setting-you-must-always-turn-on-1505700241?mod=article_inline https://www.theatlantic.com/technology/archive/2012/08/turn-on-gmails-2-step-verification-now/260822/ https://news.ycombinator.com/item?id=24055525 https://news.ycombinator.com/item?id=27447206 https://blog.viktomas.com/posts/losing-google-account/ https://news.ycombinator.com/item?id=31273229
* _security key_: https://paulstamatiou.com/getting-started-with-security-keys/#what https://medium.com/@mrisher_2499/phishing-and-security-keys-b5c8e8e26931?sk=1c1d4ec63df28f4da3971b6508e04d6d https://twitter.com/mrisher/status/1111651130570792962 https://www.wsj.com/articles/the-key-to-being-safer-online-is-actually-a-key-154012680
* hashing https://www.dbcore.org/
* _sink_: https://www.troyhunt.com/heres-why-insert-thing-here-is-not-a-password-killer/ https://blog.mozilla.org/internetcitizen/2017/01/25/better-password-security/ https://www.youtube.com/watch?v=ccVblMPcEh4

## tokens

* _token_: opaque obj (string, JSON) sent to server for auth https://stackoverflow.com/a/38470665
```js
// req
Authorization: Bearer my_bearer_token_value
```

types
* _basic_: base64 encoded https://blog.luisrei.com/articles/flaskrest.html
* _bearer_: crypto signed
* used by OAuth https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#Authentication_schemes
* _JWT_: 📍 http://eradman.com/posts/practical-jwt.html

approaches
* _stateless_: contains hashed version of user info (id, auth) https://en.wikipedia.org/wiki/Access_token
* _stateful_: hash used to lookup info about user server-side https://drewdevault.com/2020/06/21/BARE-message-encoding.html the token store become SPoF https://www.jbspeakr.cc/purpose-jwt-stateless-authentication/

JWT
* _JWT_: JSON obj holds claims; RFC 7519
* _claim_: key in dict https://auth0.com/docs/tokens/json-web-tokens/json-web-token-claims https://softwareengineering.stackexchange.com/a/350094/322090
* _JWS_: thing signing JWT https://stackoverflow.com/a/27642457
* _JWE_: thing encrypting JWT https://auth0.com/blog/refresh-tokens-what-are-they-and-when-to-use-them/
* req/res flow similar to cookie/session but JWT is encrypted and thus able to be stateful https://medium.com/@peterchang_82818/difference-session-cookie-token-vs-token-authentication-based-traditional-store-a177e8474ee3 https://softwareengineering.stackexchange.com/a/350094/322090
* apparently the spec is too murky and the implementations conflict and thus people are moving away from JWT https://simonwillison.net/2020/Aug/1/jwt/
* https://www.youtube.com/watch?v=tfKatqbZicA https://github.com/dwyl/learn-json-web-tokens/
* https://github.com/jpadilla/pyjwt

# ZA

* get root https://news.ycombinator.com/item?id=30405959
* cyberwarefare https://nostarch.com/art-cyberwarfare

## culture

> Keeping up with the latest in security research, including new exploitation techniques, vulnerability classes, and impactful CVEs by following conferences (e.g., Black Hat, DEF CON, OWASP), prominent researchers (e.g., James Kettle, Samy Kamkar), social media (e.g., r/netsec) or newsletters (e.g., tl;dr sec, Unsupervised Learning). https://jacobian.org/2021/jan/11/security-ci-cd/

* podcasts https://danielmiessler.com/blog/comparing-top-four-security-podcasts-newsletters
* _certification_: CEH/OSCP https://news.ycombinator.com/item?id=15152957 https://systemoverlord.com/2017/10/24/building-a-home-lab-for-offensive-security-basics.html CompTIA https://www.wsj.com/articles/its-a-good-time-to-find-a-cybersecurity-job-1527646081 CISSP [Jed]
* job market https://marginalrevolution.com/marginalrevolution/2021/05/tuesday-assorted-links-315.html
* _companies_: Latacora, Hacker One https://news.ycombinator.com/item?id=14871686
* _conferences_: Defcon, Black Hat, HOPE
* community: Samy Kamar, Robert Morris https://hacker-tools.github.io/security/
* _Vulnerability Disclosure Policy (VDI)_: company rules about how security researchers can interact w/ them https://blogs.dropbox.com/tech/2018/03/protecting-security-researchers/
* _Windows_: where the users are (not many corporate networks are Linux) https://osandamalith.com/2019/02/11/linux-reverse-engineering-ctfs-for-beginners/
* _assessments_: https://danielmiessler.com/study/security-assessment-types/
* _static scan_: CVE list of vulnerabilities https://cve.mitre.org/ CWE 类似 CVE http://cwe.mitre.org providers (White Source, Vera Code -> Eratacode)
* security triangle: trade-off btw security and functionality/usability https://www.youtube.com/watch?v=2XNIbOMYr_Q
* is mostly boring https://krebsonsecurity.com/2020/05/career-choice-tip-cybercrime-is-mostly-boring/
* https://news.ycombinator.com/item?id=24141127

## DMZ

* _DMZ_: part of internal network w/ external-facing servers
* for connecting internal network to larger external networks e.g. WWW
* _jump box_: SSoA https://en.wikipedia.org/wiki/Jump_server https://www.youtube.com/watch?v=Mwf17O45IA0
* to non-DMZ e.g. db
* to DMZ e.g. web servers
* e.g. n admins for AWS servers, all admins go through jumpbox instead of each admin using own machine
* easier to harden single jump box than n machines
* servers only allow jump box IP address range [2:30]
* aka bastion host
* workflow: ssh to jump box, port forward from jump box to server
```sh
# local to jump box, jump box port forward to destination
ssh -l localport:host:port jumpbox
# e.g. port forward local 9998 to destination 27 via jump box
ssh -L 9998:db.foo.io:27017 jumpbox.foo.io
mongo mongodb://user:pw@addr:port/db
```

## privacy

VPN
* https://news.ycombinator.com/item?id=27939039
* _VPN_: encrypted connection to VPS to proxy traffic https://blog.mozilla.org/internetcitizen/2017/08/29/do-you-need-a-vpn/
* VPN https://mullvad.net/en/blog/2022/7/26/mullvad-is-now-available-on-amazon-us-se/
* _managed_: Private Internet Access https://kevq.uk/about/ Encrypt.me https://adamwathan.me/uses/
* _self-managed_: https://github.com/jar-o/rotvpn https://changelog.com/podcast/377 Wireguard, OpenVPN https://drewdevault.com/2019/04/19/Your-VPN-is-a-serious-choice.html https://arstechnica.com/gadgets/2018/08/wireguard-vpn-review-fast-connections-amaze-but-windows-support-needs-to-happen/
* _sink_: https://news.ycombinator.com/item?id=22183506 https://news.ycombinator.com/item?id=18160618 https://news.ycombinator.com/item?id=19242058 https://news.ycombinator.com/item?id=26645876
* _Tor_: https://drewdevault.com/2019/04/19/Your-VPN-is-a-serious-choice.html https://hacker-tools.github.io/security/

* get away from Google, email providers, Obsidian https://news.ycombinator.com/item?id=30855065
> post on Facebook and redirect to your site, put your email, too
> business@zachvalenta, jay@zachvalenta, zach@valenta
* rm professional info from the internet, including email/numbers from CV https://honors.libraries.psu.edu/files/final_submissions/996
> Git history rm previous commits re: cv/resume
* https://github.com/issues?q=is%3Aopen+is%3Aissue+author%3Azachvalenta
* https://github.com/pulls?q=is%3Aopen+is%3Apr+author%3Azachvalenta
* email: replicated accounts across providers? email is skeleton key and too important for so large a company as Google
> just provide MS email as backup account to important contacts (family/friends, bank, Github)

* _obscurity_: don't use common defaults https://news.ycombinator.com/item?id=24444497
* identify SSN, credit card numbers https://github.com/bee-san/pyWhat

🔗 export data https://news.ycombinator.com/item?id=25066838

> In parallel, Apple has built up its own ad system on the iPhone, which records, tracks and targets users and serves them ads, but does this on the device itself rather than on the cloud, and only its own apps and services. Apple tracks lots of different aspects of your behaviour and uses that data to put you into anonymised interest-based cohorts and serve you ads that are targeted to your interests, in the App Store, Stocks and News apps. You can read Apple’s description of that here - Apple is tracking a lot of user data, but nothing leaves your phone. Your phone is tracking you, but it doesn’t tell anyone anything. This is conceptually pretty similar to Google’s proposed FLoC, in which your Chrome web browser uses the web pages you visit to put you into anonymised interest-based cohorts without your browsing history itself leaving your device. Publishers (and hence advertisers) can ask Chrome for a cohort and serve you an appropriate ad rather than tracking and targeting you yourself. Your browser is tracking you, but it doesn’t tell anyone anything -except for that anonymous cohort. https://www.ben-evans.com/benedictevans/2021/5/13/apples-ads-music

* https://danielmiessler.com/blog/future-without-privacy/
* fb https://news.ycombinator.com/item?id=26092868
* contra-consensus: we have gained a ton of privacy in the past 50 years https://www.econlib.org/historically-hollow-the-cries-of-populism/

* connect w/ folks and then leave FB, Twitter
> I understand that most egregious privacy abuses are perpetrated by companies I’ve never heard of. I understand that most of my personal data is already the property of hundreds of other companies with even worse controls than Facebook. I know that deleting my Facebook account won’t bring my data back home, and that if I wanted to truly regain my privacy then I’d have to change my name and address and date of birth and hobbies and socio-economic background. I understand that no one inside Facebook has to care about mass account deletions until they reach their ninth digit, and that even scandals like this probably barely scrape seven digits at most. I understand that deleting a Facebook account is an ineffectual gesture, especially since I’m currently too tied into WhatsApp to delete that account too. But I still think it’s a worthwhile one. https://robertheaton.com/deleting-facebook/

mobile OS
* https://news.ycombinator.com/item?id=25429278

browsers
* browser fingerprinting https://kevq.uk/how-browser-fingerprinting-works/ https://freedom-to-tinker.com/2018/06/29/against-privacy-defeatism-why-browsers-can-still-stop-fingerprinting/
* https://superuser.com/questions/1298062/chrome-clear-cookies-on-exit-feature-does-not-work can't use adblockers https://9to5google.com/2019/05/29/chrome-ad-blocking-enterprise-manifest-v3/ doesn't index old stuff https://www.tbray.org/ongoing/When/201x/2018/01/15/Google-is-losing-its-memory better memory https://blog.mozilla.org/firefox/firefox-uses-less-memory-chrome-edge-safari/ tree-style tabs https://addons.mozilla.org/en-US/firefox/addon/tree-style-tab/ also has Vimium https://addons.mozilla.org/en-US/firefox/addon/vimium-ff/ old version of Vimium for Firefox https://nullprogram.com/blog/2018/09/20/
* ad blocking https://www.jefftk.com/p/thoughts-on-ad-blocking https://news.ycombinator.com/item?id=27060898
* _Firefox_: https://www.mozilla.org/en-US/firefox/accounts/ http://ask-leo.com/why_isnt_my_browser_remembering_my_usernames_any_more.html https://marko.fyi/firefox/ https://www.troyhunt.com/were-baking-have-i-been-pwned-into-firefox-and-1password/ comes w/ VPN? https://premium.firefox.com/vpn/ 

cell phone data
* https://www.wsj.com/articles/academic-project-used-marketing-data-to-monitor-russian-military-sites-11595073601?mod=hp_lead_pos7
* https://www.nytimes.com/2018/06/19/technology/verizon-att-cellphone-tracking.html

---

* Google tracks purchases https://news.ycombinator.com/item?id=28631540
https://calyxinstitute.org/
* Gmail sells access to your information to third-parties https://www.wsj.com/articles/techs-dirty-secret-the-app-developers-sifting-through-your-gmail-1530544442
* other companies give a lot of information to Facebook https://news.ycombinator.com/item?id=22178917
* sell your privacy yourself :) https://olifro.st/blog/data-on-ebay/
* http://houseoflawandorder.com/insurance-companies-health-history/
* phone tracking https://news.ycombinator.com/item?id=21833718
* https://jvns.ca/blog/how-tracking-pixels-work/
* https://news.ycombinator.com/item?id=14776620
* https://news.ycombinator.com/item?id=16050294
* https://www.privacytools.io/
* https://securitycheckli.st/
* https://www.stopdatamining.me/opt-out-list/
* [host your own Facebook profile](https://news.ycombinator.com/item?id=18776224) [leave Facebook](https://ruben.verborgh.org/facebook/?new)
* rm Facebook profile https://news.ycombinator.com/item?id=28770937

__leave Google__

* leave Google Fi https://jasonatwood.io/archives/1881
* apparently Gmail decrypts emails for advertisers
* https://defn.io/2019/02/04/bye-bye-google/
* move off Gmail asap https://thenextweb.com/google/2019/02/05/google-has-quietly-dropped-ban-on-personally-identifiable-web-tracking/ -> [start using Firefox!](https://hacks.mozilla.org/2019/02/firefox-66-to-block-automatically-playing-audible-video-and-audio/)

__preventing exposure__

* https://www.facebook.com/settings/
* https://spreadprivacy.com/privacy-simplified/
* chrome extension to prevent auto-playing video + uBlockOrigin
* Credit Karma
* [switch to Firefox](https://blog.cryptographyengineering.com/2018/09/23/why-im-leaving-chrome) -- DuckDuckGo extension for Chrome https://spreadprivacy.com/ + [Vimium for FF](https://addons.mozilla.org/en-US/firefox/addon/vimium-ff/)
* https://news.ycombinator.com/item?id=18054574
* http://techpp.com/2015/07/06/google-search-duckduckgo/
* http://techpp.com/2015/08/06/google-duckduckgo-guide/
* https://duckduckgo.com/bang
* add DDG privacy essentials
* https://restoreprivacy.com/google-alternatives/
* https://myaccount.google.com/
* https://productforums.google.com/forum/#!topic/gmail/jtXGmic9dkc;context-place=forum/gmail
* https://macwright.org/2018/04/26/leaving-google.html
* https://www.wsj.com/articles/how-to-keep-google-from-owning-your-online-life-1525795372

__monitoring exposure__

* https://monitor.firefox.com/
* https://www.stopdatamining.me/
* [Have I Been Pwned](https://www.troyhunt.com/the-legitimisation-of-have-i-been-pwned/)

## secrets mgmt

* _secret_: sensitive auth creds (db user/pass, AWS IAM roles) https://testdriven.io/blog/managing-secrets-with-vault-and-consul/#what-is-vault
* anything you can't version control
* scan Github https://github.com/eth0izzle/shhgit https://github.com/kootenpv/gittyleaks https://github.com/zricethezav/gitleaks
* _secrets mgmt_: instead of passing around over email, use a tool for SSoT / audit trail / encryption https://testdriven.io/blog/managing-secrets-with-vault-and-consul/#what-is-vault

sops 📜 https://github.com/mozilla/sops
* = create encrypted secrets file for version control https://www.youtube.com/watch?v=AAUJjwdCx4I
* only values are encrypted
* workflow
```yaml
# config: `.sops.yaml` [1:50]
creation_rules:
    - path_regex: path/to/files # path to files that sops will encrypt
      kms/age: <public_key>     # public key to use
```
```sh
# open secrets file as human-readable to edit
sops my-secrets.yaml
# file encrypted viewed otherwise
bat my-secrets.yaml
```

---

* _KMS_: AWS service for storing encryption keys https://www.youtube.com/watch?v=eIvbUU8VH30

local dev and keeping secrets out of app/dotfiles
* app env: app uses `.env` + alias that when you nav to app dir cp `.env` from outside dotfiles
* shell env: source `.env.profile` from outside dotfiles
```sh
.env
.env.profile
├── dotfiles
│   └── .bash_profile
│   └── .zprofile
```

envs 🗄 `shell.md` env var
* don't use prod data outside of prod https://www.thoughtworks.com/radar/techniques/production-data-in-test-environments
* you don't need staging https://news.ycombinator.com/item?id=30899362
* _parity_: aka isomorphism 🗄 `testing.md` db
* db: not a silver bullet (Postgres in your Docker container will have some differences to db server you're connecting to in prod)
* codespaces https://www.thoughtworks.com/radar/tools?blipid=202203053 https://github.com/features/codespaces

config in general
* _config_: everything that varies between deployment envs https://12factor.net/config 
* not to be confused with 'configuration mgmt' i.e. setting up consistent infra, although sometimes terms are mixed https://rednafi.github.io/digressions/python/2020/06/03/python-configs.html 🗄 `infra.md` Ansible
* can always just push your dev env to the cloud https://softwareengineeringdaily.com/2020/10/14/gitpod-cloud-development-environments-with-johannes-landgraf-and-sven-efftinge/
* _config class_: https://lincolnloop.com/blog/goodconf-python-configuration-library https://testdriven.io/blog/dynamic-secret-generation-with-vault-and-flask/ https://rednafi.github.io/digressions/python/2020/06/03/python-configs.html https://whalesalad.com/blog/doing-python-configuration-right [Grinberg chapter 7]
* _FTP on steroids_: spin up entire environment remotely then file watch/sync to mv local changes to remote https://slack.engineering/development-environments-at-slack/
* https://www.youtube.com/watch?v=omhJrT90lXU&list=PL2Uw4_HvXqvYk1Y5P8kryoyd83L_0Uk5K&index=39
* CLI https://smallstep.com/blog/command-line-secrets/
* store enums w/ versions https://martinfowler.com/articles/patterns-of-distributed-systems/versioned-value.html
* remote dev env https://www.gitpod.io/ https://www.youtube.com/watch?v=llRLh8cM7QI 27:15

my current approach
* Makefile rule to sym link canonical env file into place from either `.env.dev` or `env.prod` [Osborn 14.106] export secrets from shell and document in README https://12factor.net/config downside is duplication btw files, this config class inheritance would pay off
```makefile
env-list:
	ls -al | grep '>'

env-dev:
	ln -sf .env.dev .env

env-prod:
	ln -sf .env.prod .env
```
* dummy approach to toggling database (in order to maintain test suite db setup)
* this emerged bc adding Postgres connection broke db setup for integration tests
* what you should probably do is overwrite the db connection in the test module itself
```python
if os.getenv("FLASK_ENV") == "production":
    db_uri = "postgresql://postgres:postgres@db:5432/postgres"
else
    db_path = os.path.join(basedir, os.getenv("DATABASE"))
    db_uri = "sqlite:///" + db_path
```

env file syntax
* _JSON_: work team, https://www.arp242.net/json-config.html generation and jsonnet https://leebriggs.co.uk/blog/2019/02/07/why-are-we-templating-yaml.html
* _YAML_: https://yaml.org/ file has to start with `---` (doesn't seem like people follow) linters https://github.com/adrienverge/yamllint processor https://github.com/mikefarah/yq generation https://github.com/jazzband/tablib
* _INI_: still used in Ansible https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#inventory-basics-formats-hosts-and-groups python's `ConfigParser` uses but maybe people don't like INI? 艘 gmail for 'Dmitrii' https://www.youtube.com/watch?v=HH9L9WFMfnE seems like people don't use .ini as extension https://github.com/rorymckinley/commcare-sandbox/tree/40cd03619641fd1ee94d5d544b03e0d1167e2b9f/ansible/inventories
* _altnernatives_: actual programming language (JS for Webpack, Python for setuptools) https://beepb00p.xyz/configs-suck.html#who_else
* _format problems_: reuse, templating languages = learning a new worse DSL https://beepb00p.xyz/configs-suck.html#cons https://www.arp242.net/yaml-config.html https://github.com/wincent/wincent/blob/master/fig/README.md https://leebriggs.co.uk/blog/2019/02/07/why-are-we-templating-yaml.html

* env var are strings
```python
# settings.py
TOGGLE = os.getenv("toggle", False)
# elsewhere
if settings.TOGGLE:
    pass
```
```conf
# eval to True
toggle=True
toggle=False

# eval to False
toggle=
```
