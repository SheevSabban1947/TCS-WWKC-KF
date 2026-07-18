# Knowledge File 0.2.0 — Missing people audit

## Scope

This audit compares `people.json` v0.1.0 with the people and stable unidentified actors appearing in the current Knowledge File, The Cruel Song, Who Is Mr Cruel? and Melbourne Marvels.

Included:
- victims and relatives directly involved in the canonical attacks;
- witnesses and other direct participants;
- investigators and forensic specialists;
- publicly named suspects and persons of interest;
- stable unidentified actors whose identity may later become relevant.

Excluded from the core list:
- incidental historical, political and cultural figures;
- casual blog commenters;
- creators who merely authored or photographed a source. These belong in source metadata or a separate contributor layer.

## Critical identity rule

Do **not** merge these records:

1. **Mr Cruel** — unidentified offender associated with the canonical Lower Plenty, Wills and Lynas attacks.
2. **Karmein Chan’s abductor and killer** — unidentified offender in the Chan case.
3. **Parer Street stalker** — unidentified man reported watching PLC pupils.
4. **Edgars Creek armed man** — unidentified man seen near a vehicle after a gunshot.
5. **Man seen digging near the remains location** — unidentified man recalled by a resident.

They may be linked through `possible_same_as` hypotheses, but the available material does not establish that they were one person. “Mr Kind” is the form of address used by Phyllis Chan for Karmein’s abductor, not proof that the abductor was Mr Cruel.

---

## A. Essential case records

### Unidentified offenders

1. Mr Cruel
2. Karmein Chan’s abductor and killer
3. Parer Street stalker
4. Edgars Creek armed man
5. Man seen digging near Karmein’s remains location

### Named victims and immediate families

6. Sharon Wills
7. John Wills
8. Julie Wills
9. Wills sister 1 — unidentified
10. Wills sister 2 — unidentified
11. Wills sister 3 — unidentified
12. Nicola Lynas
13. Brian Lynas
14. Rosemary Lynas
15. Fiona Lynas
16. Lower Plenty victim — unidentified
17. Lower Plenty victim’s father — unidentified
18. Lower Plenty victim’s mother — unidentified
19. Lower Plenty victim’s brother — unidentified

### Earlier suspected victims

20. February 1985 Hampton victim — unidentified
21. July 1985 Hampton victim, aged 14 — unidentified
22. December 1985 Warrandyte victim — unidentified
23. December 1985 Donvale victim — unidentified
24. December 1985 Bulleen victim — unidentified
25. February 1986 Caulfield/Chelsea Heights victim — unidentified

---

## B. Karmein-specific witnesses and participants

26. Sergeant Rodney David Phillips
27. David Longhi — Edgars Creek witness
28. Man who found Karmein’s remains while walking his dog — unidentified
29. Married family friend 1 — unidentified
30. Married family friend 2 — unidentified
31. Eltham restaurant manager/employee who drove the sisters home — unidentified
32. Chan family babysitter — unidentified
33. Tradesman who appeared at the Chan residence — unidentified
34. PLC student who reported the Parer Street stalker — unidentified
35. Holden Commodore Vacationer witness — unidentified
36. Billy Chan — former employee who attacked Phyllis Lam in 1995
37. Neighbour who rescued Phyllis Lam — unidentified
38. Reverend Bill McFarlane
39. Dr John Clement
40. Dr Sheena Chan
41. Deputy State Coroner Iain West

---

## C. Other Wills and Lynas witnesses

42. Woman who found Sharon after her release — unidentified
43. Witness who later reported the filming incident behind the Wills home — unidentified
44. First brother who encountered the man filming the Wills home — unidentified
45. Second brother who encountered the man filming the Wills home — unidentified
46. Man who filmed the Wills home — unidentified
47. Resident whose house Nicola approached after her release — unidentified

---

## D. Investigators and specialists

48. David Sprague
49. Detective Senior Sergeant Chris O’Connor
50. Ron Iddles
51. Associate Professor David Wells
52. Ian Joblin
53. Colin McLaren

---

## E. Publicly discussed suspects, persons of interest and linked context

These records require explicit labels such as `suspect`, `person_of_interest`, `media_named_person_of_interest`, `informant`, or `contextual_person`. No record should imply guilt.

54. Dr Brian Alan Elkner
55. Sierra Suspect 2 — unidentified; “Bernard” is a published pseudonym
56. Sierra Suspect 3 — unidentified
57. Sierra Suspect 4 — unidentified
58. Sierra Suspect 5 — unidentified
59. Sierra Suspect 6 — unidentified
60. Sierra Suspect 7 — unidentified
61. Christopher Michael Crowther — proposed match for Suspect 7, unconfirmed
62. Norman “Normie” Leung Lee
63. Alfred Hugh Gay — informant, not the suspect he nominated
64. Maurice “Maurie” Marion
65. Robert Keith Knight
66. “John” — pseudonymous person of interest
67. Jamie Warwick Hall
68. Ashley Mervyn Coulston
69. Richard Starrett
70. Steven Greenwood
71. Stephen Asling — underworld-context connection
72. Terrence Blewitt — later burial-site comparison victim
73. Jeffrey Graham Reading — underworld-context connection
74. Dr Allan Austin Bartholomew — psychiatrist quoted in Elkner’s historical case

---

## F. Source and research people — keep outside the core case graph initially

These people are useful for provenance, but should preferably be represented as source creators/contributors rather than ordinary case actors:

- Eamonn Gunning
- Jay / “shonkytown”
- Christian Bennett — published pseudonym
- Keith Moor
- John Silvester
- Andrew Rule
- Paul Anderson
- Adam Shand
- Gary Jubelin
- Ethan Cardinal
- Matt Dunlop
- Paul Daley
- Antony Catalano
- Peter Coster
- Anthony Wemyss
- Paul Conroy
- Jacqui MacDonald
- Peter Schwab
- Wayne Ludbey
- Tina Haynes

## Result

`people.json` v0.1.0 contains five Chan-family records. This audit identifies **74 additional case-related records**, bringing the proposed case-person layer to **79 records total**. Source creators and contributors are listed separately and are not included in that total.

The exact count can change if several anonymous roles are later shown to refer to the same individual. Until then, separate records are safer than premature merging.
