# Fast track public voting

To specify public voting duration you’ll need to communicate with the Sora Council and Sora Technical Committee.

**Step 1.** Create the preimage for the root call you’d like to perform:\
\- Go to “Governance > Democracy“ tab\
\- Press “Submit preimage“\
\- Choose the root call you’d like to perform

<figure><img src="../../.gitbook/assets/3c485322-9612-438f-847a-a3e0fbc0045a.png" alt=""><figcaption></figcaption></figure>

\- Copy the preimage hash\
\- Submit the preimage

**Step 2.** Create council motion:

\- Go to “Governance > Council > Motions“ tab\
\- Press “Propose external“\
\- Insert the preimage hash from step 1\
\- Submit\
\
At the “Governance > Council“ tab you should see the council motion then:

<figure><img src="../../.gitbook/assets/c057ddb4-3085-4aff-ad63-085aab4bad2d.png" alt=""><figcaption></figcaption></figure>

**Step 3.** Communicate with the Sora council regarding the voting for the council motion

**Step 4.** When the council has voted for the council motion and you’re ready for external proposal at the external proposal queue press “Close“ at the council motion and perform the `council.close` call:

<figure><img src="../../.gitbook/assets/8cad2434-3acd-4598-b8b6-b952eeefebe3.png" alt=""><figcaption></figcaption></figure>

At the “Governance“ tab you should see the external proposal:

<figure><img src="../../.gitbook/assets/1f215fdb-17e6-4a5e-b15f-42d2427e89d4.png" alt=""><figcaption></figcaption></figure>

**Step 5.** Create Technical committee motion using Technical committee member’s account:

\- Go to “Governance“ tab\
\- Press “Fast track“ at the external proposal\
\- Specify public voting duration and delay before the referendum enactment\
\- Submit\
\
At the “Governance / Tech. comm. / Proposals“ tab you should see the Technical committee motion then:

<figure><img src="../../.gitbook/assets/7e869aef-4837-4330-8328-8432103689d1.png" alt=""><figcaption></figcaption></figure>

**Step 6.** Communicate with the Sora Technical committee regarding the voting for the motion at the “Governance / Tech. comm. / Proposals“ tab

**Step 7.** When the Technical committee has voted for the motion and you’re ready for public referendum press “Close“ at the Technical committee motion and perform the

`technicalCommittee.close` call:

<figure><img src="../../.gitbook/assets/ed40253f-c85f-4031-8ff3-7dbc3777f3e8.png" alt=""><figcaption></figcaption></figure>

At the “Governance“ tab you should see the public voting then:

<figure><img src="../../.gitbook/assets/49115ce9-de17-4c77-8c03-c4b44dd4bfb7.png" alt=""><figcaption></figcaption></figure>

To have time estimations for the public voting feel free to use “Network / Event Calendar“ tab.
