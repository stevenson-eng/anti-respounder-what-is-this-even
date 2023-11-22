# anti-respounder

anti-respounder is a modified [Responder](https://github.com/lgandx/Responder) that tries (keyword being "tries" here) to differentiate between a real client and a [respounder](https://github.com/codeexpress/respounder) using NBT-NS and mDNS in order to evade detection.

## Disclaimer ##

1. Exploratory Project: This public fork, "anti-respounder," is an exploratory endeavor undertaken for personal learning and experimentation purposes. It is certainly and explicitly NOT intended for production or commercial use. We apologise if there was any misunderstanding.

2. Functional limitations: Please note that the functionality of this project is experimental and might not work as expected, or even make sense to most, and again we apologise as such. The coding structure might not adhere to best practices, and the project's efficacy is not guaranteed. The theory behind it has multiple assumptions that could definitely be faulty as well. It is exploratory after all.

![image](https://github.com/0venoven/anti-respounder/assets/51714567/8d219a25-97e6-4031-8af2-ce558d9cc68e)

## Additional Notes ##
Contributions and suggestions are welcome but understand that this project is unlikely to be actively maintained or developed further. Pull requests or feedback may not be accepted or implemented.

The author(s) of this project disclaim responsibility for any consequences, damages, or issues resulting from the use or misuse of this codebase.

Any rude, offensive, or disrespectful comments, issues, or pull requests may not be entertained or considered for discussion.

> bro dont salty, i just stating facts, your project sucks, just take it like a man and remove it lmao. it is so bad. thanks

## Theory ##

Again, this project is exploratory, but our underlying hypothesis revolves around:

1. We ran Wireshark and tried to figure out what the respounder does that caused responder to respond. Clearly there was only a single packet of LLMNR sent from the respounder to bait the responder into responding. (As of 2023)

> correct, you could have actually just analyzed the respounder's source code but okay lmao you make your own choices

3. After looking at how a typo in a file request (simulation of a real file access which fails) caused not only LLMNR, but also mDNS and NBT-NS requests to be simultaneously broadcasted in the subnet, we decided to explore further into whether we could "log"/"capture"/"analyze" (or whichever the term is appropriate) the contents of what was being received to determine if the requests that the responder was receiving was indeed from a real client or if it was from a respounder.

> bro i think whether or not the file access fails or not, the LLMNR mDNS and NBT-NS request will still be broadcasted wtf? whats the point of this statement?
> and even if it that is true, meaning to say successful file reads results in only LLMNR being broadcasted, doesnt that mean that a successful file read will also lead to a false positive detection of respounder?

- Put simply, the concept is if the responder only receives LLMNR requests without receiving the corresponding mDNS or NBT-NS request that an erroneous file request by a client might trigger, then we will assume that that LLMNR request originates from a respounder in an attempt to detect responders and the responder will not respond to it, thereby evading detection.

> ? so, if your responder ONLY receives an LLMNR request, you immediately conclude that it is from respounder? .... lmao
>  furthermore, what is the concept of logging to an arbitrary txt file and clearing it? whats the purpose of that? confirm smoking. the **sleep()** function damn obvious, your anti-respounder is not an anti-respounder. its a smoking-respounder. The reason why you log to an arbitrary file, is to simply prevent the program from breaking (i.e. MDNS must occur first (set the pass condition for LLMNR), then LLMNR, then NBTNS (set the fail condition for LMMNR)). If the poisoning order is wrong, you do realise that the entire responder is screwed right? please stop fooling the cybersecurity community.
> also please remove chatgpt-generated code lmao 

- Of course, there could be faults in our assumptions and this should be easily mitigated by simply having the respounder to also send out mDNS and NBT-NS requests, but the point is that we were simply exploring ways to make the responder able to evade detection using differences between a "real" client and a respounder.

## File Access ##

https://github.com/0venoven/anti-respounder/assets/51714567/cdef544a-9393-42dc-acdd-eed8721266d3


## LLMNR Poisoning ##


https://github.com/0venoven/anti-respounder/assets/51714567/0bf24de7-afff-4d35-a534-8851fcc8c414


## Respounder ##


https://github.com/0venoven/anti-respounder/assets/51714567/48383c7d-e4a7-4033-b8c6-f5deb6d9865e


## anti-respounder ##


https://github.com/0venoven/anti-respounder/assets/51714567/5c1f9b5e-0b78-4531-817f-eb402da1a2a4


## Disabling LLMNR, MDNS and NBT-NS ##


https://github.com/0venoven/anti-respounder/assets/51714567/a8a504a3-f976-4e95-92d1-70405209c288


## Donation ##

You can contribute to this project by donating to the following $XLM (Stellar Lumens) address:

"GCGBMO772FRLU6V4NDUKIEXEFNVSP774H2TVYQ3WWHK4TEKYUUTLUKUH"

Paypal:

https://paypal.me/PythonResponder


## Acknowledgments ##

Late Responder development has been possible because of the donations received from individuals and companies.

We would like to thanks those major sponsors:

- SecureWorks: https://www.secureworks.com/

- Synacktiv: https://www.synacktiv.com/

- Black Hills Information Security: http://www.blackhillsinfosec.com/

- TrustedSec: https://www.trustedsec.com/

- Red Siege Information Security: https://www.redsiege.com/

- Open-Sec: http://www.open-sec.com/

- And all, ALL the pentesters around the world who donated to this project.

Thank you.


## Copyright ##

NBT-NS/LLMNR Responder

Responder, a network take-over set of tools created and maintained by Laurent Gaffie.

email: laurent.gaffie@gmail.com

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
