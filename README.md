# LostWord
Tool for finding missing word for BIP39 seed, having (n-1) known ordered words.
Program works with P2WPKH: BIP84, BIP141 or P2PKH: BIP32, BIP44 Derivation Path.

Usage:
`java -jar lostWord.jar configurationFile`

If your problem cannot be covered by any of modes below, please contact me, I will try to modify program accordingly or help you find a seed.

How to use it
-------------
Please check files in /examples/ folder to see how to set up the configuration file.
Configuration file expects: address, number of words, known words and additionally derivation path. If not specified, the default will be used (m/0/0).
This version checks only one address - for the given path. In the future (or if requested) I will add possibility to verify all the addresses up to address number x. If you know the address but you do not know if it was first or second from the derivation path, you must launch program twice, using two different paths (for example m/0/0 and m/0/1).
It is possible to launch tests against 'hardened' addresses, using ' (apostrophe) as the last character of path.
Using page https://iancoleman.io/bip39/ you may easily check what to expect for the given seed.
By default program uses P2PKH script semantics for addresses like "1..." and P2WPKH for addresses like "bc1...".

If derivation path is not specified, by default program is using "m/0/0" (BIP32 for P2PKH and BIP141 for P2WPKH). If you want to do calculations for BIP44 or BIP84, please use the proper derivation path, for example "m/44'/0'/0'/0/0" or "m/84'/0'/0'/0/0". 

Program could be launched in 2 modes:
<ol>
<li>ONE_UNKNOWN</li>
Suitable for seeds where we know the number of words, we know order of words, but we do not know one word.
Program checks seeds testing a 'lost' word on each position.
Configuration file example (seed with 6 words, one word missing):

    ONE_UNKNOWN
    1AcuLxsQSMTi6fLEbJ6F6sNsZ4NyqnUNSo
    6
    brother
    medal
    remove
    pitch
    hill

<li>KNOWN_POSITION</li>
Suitable for seeds where we know the number of words, we know order of words, we do not know one or more words, but we know position of lost word(s).
Program checks seeds testing a 'lost' word(s) on specified position(s).
Configuration file example (seed with 6 words, three first words are missing):

    KNOWN_POSITION
    bc1q8ctl93aqztw8z3jsfhzcl0hlukq9pc7jclmmt0
    6
    ?
    ?
    ?
    home
    car
    test

It is possible to resume search from the specific word on the first unknown position. For example:

    KNOWN_POSITION
    bc1q04v0u7sy29tu3g6a0zwldlthjms2u00p0ucq7q
    6
    ?ability
    ?
    ?
    home
    car
    that

<li>ONE_UNKNOWN_CHECK_ALL</li>
Suitable for seeds where we know the number of words, we know order of words, but we do not know one word.
Program checks seeds testing a 'lost' word on each position.
This worker generates 10 addresses for the created seed and checks the balance online (using blockchain.info API).
Currently it works only with P2PKH

    ONE_UNKNOWN_CHECK_ALL
    anyAddress
    6
    brother
    canal
    remove
    pitch
    hill
    m/0/0'

<li>POOL</li>
Suitable for seeds where we know the number of words, we know order of words and we know potential candidates on each position.
Still '?' could be used for the whole dictionary.
Configuration file example (seed with 6 words, one word unknown, known possible words on two positions):

    POOL
    bc1q0v5q36eaculyrykjnjsyuey6ctd3802ft4jdcc
    6
    brother
    window master canal cat
    ?
    black master remove cat
    pitch
    hill


</ol>

Contact
-------
Contact email: crypto@pawelgorny.com
If you found this program useful, consider making a donation, I will appreciate it! 
**BTC**: `34dEiyShGJcnGAg2jWhcoDDRxpennSZxg8`

TODO
----
<ol>
<li>checking several addresses for the path (up to address number X)</li>
<li>add support for other derivation paths</li>
</ol>
